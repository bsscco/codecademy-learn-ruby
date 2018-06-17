- 시작하기
    - $ rails new MySite
    - $ bundle install
    - $ rails s

- 정적 앱의 3요소
    - 컨트롤러, 라우트, 뷰

- 컨트롤러 
    - $ rails g controller Pages
    - app/controllers/pages_controller.rb
        - class PagesController &lt; ApplicationController # 컨트롤러
            - def home # 액션
            - end

        - end

    - config/routes.rb
        - Rails.application.routes.draw do
            - get 'welcome' =&gt; 'pages#home' # localhost:8000/welcome =&gt; PagesController.home

        - end

- 뷰
    - app/views/pages/home.html.erb
        - &lt;div class="main"&gt;
            - &lt;div class="container"&gt;
                - &lt;h1&gt;Hello my name is bsscco&lt;/h1&gt;
                - &lt;p&gt;I make Rails apps.&lt;/p&gt;

            - &lt;/div&gt;

        - &lt;/div&gt;

    - app/assets/stylesheets/pages.css.scss

- 정적 앱의 요청 응답 사이클
    - 1. Generate a new Rails app.
    - 2. Generate a controller and add an action.
    - 3. Create a route that maps a URL to the controller action.
    - 4. Create a view with HTML and CSS.
    - 5. Run the local web server and preview the app in the browser.

- 루트 라우트
    - config/routes.rb
        - root 'pages#home'

- 어플리케이션 레이아웃
    - app/views/layouts/application.html.erb
        - &lt;% yield %&gt;

- 동적 앱의 요청 응답 사이클
    - 1. When you type http://localhost:8000/welcome, the browser makes a request for the URL /welcome.
    - 2. The request hits the Rails router.
    - 3. The router maps the URL to a controller action to handle the request.
    - 4. The controller action recieves the request, and asks the model to fetch data from the database.
    - 5. The model returns data to the controller action.
    - 6. The controller action passes the data on to the view.
    - 7. The view renders the page as HTML.
    - 8. The controller sends the HTML back to the browser.

- 동적 앱의 4요소
    - 컨트롤러, 라우트, 뷰, 모델

- 모델
    - $ rails g model Message
    - app/model/message.rb
    - db/migrate/20150521170329_create_messages.rb
        - class CreateMessages &lt; ActiveRecord::Migration
            - def change 
                - create_table :messages do |t|
                    - t.text :content # content 필드
                    - t.timestamps # updated_at, created_at 필드

                - end

            - end

        - end

    - $ rake db:migrate
    - $ rake db:seed # 샘플 데이터 넣기

- 기본 컨트롤러 액션
    - conf/routes.rb
    - 나눠서
        - get 'messages' =&gt; 'messages#index'
        - get 'messages/new' =&gt; 'messages#new'
        - post 'messages' =&gt; 'messages#create'
        - get 'messages/:id' =&gt; 'messages#show'
        - get 'messages/:id/edit' =&gt; 'messages#edit'
        - put 'messages/:id' =&gt; 'messages#update'
        - delete 'messages/:id' =&gt; 'messages#destroy'

    - 한 번에
        - resources :messages

- 웹 템플릿
    - 변수와 흐름제어를 포함하는 HTML
    - app/views/messages/index.html.erb

- 기본 액션 구현
    - index
        - app/controllers/messages_controller.rb
            - def index
                - @messages = Message.all

            - end

        - config/routes.rb
            - get 'messages' =&gt; 'messages#index'

        - app/views/messages/index.html.erb
            - &lt;% @messages.each do |message| %&gt;
            - &lt;p class="content"&gt;&lt;%= message.content %&gt;&lt;/p&gt;
            - &lt;p class="time"&gt;&lt;%= message.created_at %&gt;&lt;/p&gt;
            - &lt;% end %&gt;

    - new
        - app/controllers/messages_controller.rb
            - def new
                - @message = Message.new

            - end

        - config/routes.rb
            - get 'messages/new' =&gt; 'messages#new'

        - app/views/messages/new.html.erb
            - &lt;%= form_for @message do |f| %&gt;
            - &lt;%= f.label :message %&gt;&lt;br&gt;
            - &lt;%= f.text_area :content %&gt;&lt;br&gt;
            - &lt;%= f.submit "Create" %&gt;
            - &lt;% end %&gt;

        - app/views/messages/index.html.erb
            - &lt;%= link_to 'New Message', 'messages/new' %&gt;

    - create
        - app/controllers/messages_controller.rb
            - def create
                - @message = Message.new(message_params)
                - if @message.save
                    - redirect_to '/messages'

                - else
                    - render 'new'

                - end

            - end
            - private
            - def message_params
                - params.require(:message).permit(:content)

            - end

        - config/routes.rb
            - post 'messages' =&gt; 'messages#create'

- 기본 라우트 한 번에 구현
    - config/routes.rb
        - resources :signups

- DB 데이터 확인
    - $ rails console
    - $ Signup.all

- 쿼리
    - @posts = Posts.order(created_at: :desc).all

- 모델 관계 설정하기
    - 1:다
        - class Tag &lt; ActiveRecord::Base
            - has_many :destinations

        - end
        - class Destination &lt; ActiveRecord::Base
            - belongs_to :tag

        - end
        - class CreateDestinations &lt; ActiveRecord::Migration
            - def change
                - create_table :destinations do |t|
                    - t.references :tag
                    - t.timestamps

                - end

            - end

        - end

- 라우트 별명 짓기
    - get 'tags/:id' =&gt; 'tags#show', as: :tag

- 기본 액션 구현
    - show
        - config/routes.rb
            - get 'tags/:id' =&gt; 'tags#show', as: :tag

        - app/controllers/tags_controller.rb
            - def show
                - @tag = Tag.find(params[:id])
                - @destinations = @tag.destinations

            - end

        - app/views/tags/index.html.erb
            - &lt;% @tags.each do |t| %&gt;
                - &lt;%= link_to tag_path(t) do %&gt;
                    - &lt;%= t.title %&gt;&lt;br&gt;

                - &lt;% end %&gt;
                - &lt;%= link_to "Learn more", tag_path(t) %&gt;

            - &lt;% end %&gt;

        - app/views/tags/show.html.erb
            - &lt;%= @tag.title %&gt;
            - &lt;% @destinations.each do |d| %&gt;
                - &lt;%= d.description %&gt;

            - &lt;% end %&gt;

    - edit
        - config/routes.rb
            - get 'destinations/:id/edit' =&gt; 'destinations#edit', as: :edit_destination

        - app/controllers/destinations_controller.rb
            - def edit
                - @destination = Destination.find(params[:id])

            - end

        - app/views/destinations/edit.html.erb
            - &lt;%= form_for @destination do |f| %&gt;
                - &lt;%= f.title %&gt;&lt;br&gt;

            - &lt;% end %&gt;

        - app/views/destinations/show.html.erb
            - &lt;%= link_to 'Edit', edit_destination_path(@destination) %&gt;

    - update
        - config/routes.rb
            - patch 'destinations' =&gt; 'destinations#update'

        - app/controllers/destinations_controller.rb
            - def update
                - @destination  = Destination.find(params[:id])
                - if @destination.update_attributes(destination_params)
                    - redirect_to action: 'show', id: @destination.id

                - else
                    - render 'edit'

                - end

            - end
            - private
            - def destination_params
                - params.require(:destination).permit(:title)

            - end

- 모델 관계 설정하기
    - 다:다
        -  class Movie &lt; ActiveRecord::Base
            - has_many :parts
            - has_many :actors, through: :parts

        - end
        - class Actor &lt; ActiveRecord::Base
            - has_many :parts
            - has_many :movies, through: :parts

        - end
        - class Part &lt; ActiveRecord::Base
            - belongs_to :movie
            - belongs_to :actor

        - end
        - class CreateParts &lt; ActiveRecord::Migration
            - def change
                - create_table :parts do |t|
                    - t.belongs_to :movie, index: true
                    - t.belongs_to :actor, index: true
                    - t.timestamps

                - end

            - end

        - end
