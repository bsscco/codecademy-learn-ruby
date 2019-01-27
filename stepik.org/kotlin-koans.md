Kotlin koans
============

introduction
------------

### simple function

fun start(): String = “OK”

### named argument

options.joinToString(prefix = “\[“, postfix =”\]”)

### default argument

fun foo(name: String, number: Int = 42, toUpperCase: Boolean = false) =
…

### lambda

fun containsEven(collection: Collection&lt;Int&gt;): Boolean =
collection.any { it -&gt; it % 2 == 0 }

### raw string & string template

fun getPattern(): String = “”“ ${month} ”“”

### data class

data class Person(val name: String, val age: Int)

### nullable type

fun sendMessageToClient(client: Client?, message: String?, mailer:
Mailer){ if (client == null || message == null) return

    val personalInfo = client.personalInfo ?: return

    val email = personalInfo!!.email ?: return

### smart cast & when expression

fun eval(expr: Expr): Int = when (expr) { is Num -&gt; expr.value is Sum
-&gt; eval(expr.left) + eval(expr.right) else -&gt; throw
IllegalArgumentException(“Unknown expression”) }

### extension function

fun Int.r(): RationalNumber = RationalNumber(this, 1)

### object expression

Collections.sort(arrayList, object : Comparator&lt;Int&gt; { override
fun compare(x: Int, y: Int) = y - x })

### SAM conversion

Collections.sort(arrayList, { x, y -&gt; y - x })

### extention function on collections

return arrayListOf(1, 5, 2).sortedDescending()

conventions
-----------

### comparison

data class MyDate(val year: Int, val month: Int, val dayOfMonth: Int)
<b>: Comparable&lt;MyDate&gt; </b>{ <b>override fun compareTo(other:
MyDate) = when { year != other.year -&gt; year - other.year month !=
other.month -&gt; month - other.month else -&gt; dayOfMonth -
other.dayOfMonth }</b> }

fun compare(date1: MyDate, date2: MyDate) = <b>date1 &lt; date2</b>

### in range

class DateRange(val start: MyDate, val endInclusive: MyDate) {
<b>operator fun contains(d: MyDate) = start &lt;= d && d &lt;
endInclusive</b> }

fun checkInRange(date: MyDate, first: MyDate, last: MyDate): Boolean {
return <b>date in DateRange(first, last)</b> }

### range to

<b>operator fun MyDate.rangeTo(other: MyDate) = DateRange(this,
other)</b>

class DateRange(override val start: MyDate, override val endInclusive:
MyDate): ClosedRange&lt;MyDate&gt;

fun checkInRange(date: MyDate, first: MyDate, last: MyDate): Boolean {
return <b>date in first..last</b> }

### for loop

class DateRange(val start: MyDate, val end: MyDate)<b> :
Iterable&lt;MyDate&gt;</b> { <b>override fun iterator():
Iterator&lt;MyDate&gt; { return object : Iterator&lt;MyDate&gt; { var
currentDate: MyDate = start;

            override fun hasNext(): Boolean {
                return currentDate &lt;= end
            }

            override fun next(): MyDate {
                val result = currentDate
                currentDate = currentDate.nextDay()
                return result
            }
        }
    }</b>

}

fun iterateOverDateRange(firstDate: MyDate, secondDate: MyDate, handler:
(MyDate) -&gt; Unit) { <b>for (date in firstDate..secondDate)</b> {
handler(date) } }

### operator overloading

data class MyDate(val year: Int, val month: Int, val dayOfMonth: Int)

enum class TimeInterval { DAY, WEEK, YEAR }

<b>operator fun MyDate.plus(timeInterval: TimeInterval): MyDate =
addTimeIntervals(timeInterval, 1) </b> class RepeatedTimeInterval(val
timeInterval: TimeInterval, val number: Int)

operator fun TimeInterval.times(number: Int) =
RepeatedTimeInterval(this, number)

<b>operator fun MyDate.plus(repeatedTimeInterval: RepeatedTimeInterval)
: MyDate = addTimeIntervals(repeatedTimeInterval.timeInterval,
repeatedTimeInterval.number)</b>

fun task1(today: MyDate): MyDate { return today + YEAR + WEEK }

fun task2(today: MyDate): MyDate { return today + YEAR \* 2 + WEEK \* 3
+ DAY \* 5 }

### destructoring declaration

<b>data class MyDate(val year: Int, val month: Int, val dayOfMonth:
Int)</b>

fun isLeapDay(date: MyDate): Boolean { <b>val (year, month, dayOfMonth)
= date</b> }

### invoke

class Invokable { var numberOfInvocations: Int = 0 private set
<b>operator fun invoke(): Invokable</b> { numberOfInvocations++ return
this } }

fun invokeTwice(invokable: Invokable) = <b>invokable()()</b>

collections
-----------

### collection extension function

fun Shop.getSetOfCustomers(): Set&lt;Customer&gt; =
<b>customers.toSet()</b>

### filter & map

fun Shop.getCitiesCustomersAreFrom(): Set&lt;City&gt; = <b>customers.map
{ it.city }.toSet()</b>

fun Shop.getCustomersFrom(city: City): List&lt;Customer&gt; =
<b>customers.filter { it.city == city }</b>

### any, all, and other predicates

fun Shop.checkAllCustomersAreFrom(city: City): Boolean =
<b>customers.all { it.city == city }</b> fun Shop.hasCustomerFrom(city:
City): Boolean = <b>customers.any { it.city == city }</b> fun
Shop.countCustomersFrom(city: City): Int = <b>customers.count { it.city
== city }</b> fun Shop.findAnyCustomerFrom(city: City): Customer? =
<b>customers.find { it.city == city }</b>

### flatmap

fun Customer.getOrderedProducts(): Set&lt;Product&gt; =
<b>orders.flatMap { it.products }.toSet()</b>

fun Shop.getAllOrderedProducts(): Set&lt;Product&gt; =
<b>customers.flatMap { it.orders.flatMap { it.products } }.toSet()</b>

### max & min

fun Shop.getCustomerWithMaximumNumberOfOrders(): Customer? =
<b>customers.maxBy { it.orders.size }</b>

fun Customer.getMostExpensiveOrderedProduct(): Product? =
<b>orders.flatMap { it.products }.maxBy { it.price }</b>

### sort

fun Shop.getCustomersSortedByNumberOfOrders(): List&lt;Customer&gt; =
<b>customers.sortedBy { it.orders.size }</b>

### sum

fun Customer.getTotalOrderPrice(): Double = orders.flatMap { it.products
}.<b>sumByDouble { it.price }</b>

### group by

fun Shop.groupCustomersByCity(): Map&lt;City, List&lt;Customer&gt;&gt; =
<b>customers.groupBy { it.city }</b>

### partition

fun Shop.getCustomersWithMoreUndeliveredOrdersThanDelivered():
Set&lt;Customer&gt; = customers.filter { <b>val (delivered, undelivered)
= it.orders.partition { it.isDelivered }</b> undelivered.size &gt;
delivered.size }.toSet()

### fold

fun Shop.getSetOfProductsOrderedByEveryCustomer(): Set&lt;Product&gt; {
val allProducts = customers.flatMap { it.orders.flatMap { it.products }
}.toSet() return <b>customers.fold(allProducts) { orderedByAll, customer
-&gt; orderedByAll.intersect(customer.orders.flatMap { it.products
}.toSet()) }</b> }

### compound collection functions

fun Customer.getMostExpensiveDeliveredProduct(): Product? =
<b>orders.filter { it.isDelivered }.flatMap { it.products }.maxBy {
it.price }</b>

fun Shop.getNumberOfTimesProductWasOrdered(product: Product): Int =
<b>customers.flatMap { it.orders.flatMap { it.products } }.count {
it.name == product.name }</b>

### compound collection functions2

fun doSomethingStrangeWithCollection(collection:
Collection&lt;String&gt;): Collection&lt;String&gt;? {

    val groupsByLength = collection. groupBy { s -&gt; s.length }

    val maximumSizeOfGroup = groupsByLength.values.map { group -&gt; group.size }.max()

    return groupsByLength.values.<b>firstOrNull { group -&gt; group.size == maximumSizeOfGroup }</b>

}

properties
----------

###
