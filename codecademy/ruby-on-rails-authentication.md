- 세션
    - 유저의 컴퓨터와 서버 간의 연결

- 패스워드 보안기능 사용
    - app/models/user.rb
        - class User &lt; ActiveRecord::Base
            - has_secure_password # bcrypt 알고리즘을 사용해 submit된 유저의 password_field 데이터를 digest 문자열로 바꾼다.

        - end

    - Gemfile
        - gem 'bcrypt', '~&gt; 3.1.7'

    - $ bundle install
    - db/migrate/XXXXXXX_create_users.rb
        - t.string :password_digest # bcrypt를 위해 약속된 컬럼명

- DB 확인
    - $ rails console
    - $ User.create(first_name: "Edna", last_name: "Mode", email: 'edna@example.com', password: 'incredibles') # password는 알아서 해시값으로 계산되어 들어감.
    - $ User.find_by(first_name: 'Edna').authenticate('incredibles') # password_digest에 들어있는 해시값과 'incredibles'를 해시로 바꾼 값을 비교한다.

- 회원가입
    - config/routes.rb
        - get '/signup' =&gt; 'users#new'
        - post '/users' =&gt; 'users#create'

    - app/views/users/new.html.erb
        - &lt;%= form_for @user do |f| %&gt;
            - &lt;%= f.text_field :first_name, :placeholder: "First name" %&gt;
            - &lt;%= f.text_field :last_name, :placeholder: "Last name" %&gt;
            - &lt;%= f.email_field :email, :placeholder: "Email" %&gt;
            - &lt;%= f.password_field :password, :placeholder: "Password" %&gt;
            - &lt;%= f.submit "Create an account" %&gt;

        - &lt;% end %&gt;

    - app/controllers/user_controller.rb
        - def new 
            - @user = User.new

        - end
        - def create
            - @user = User.new(user_params)
                - if @user.save
                    - session[:user_id] = @user.id
                    - redirect_to '/'

                - else
                    - render 'new'

                - end

            - end

- 로그인
    - config/routes.rb
        - get '/login' =&gt; 'sessions#new'
        - post '/sessions =&gt; 'sessions#create'

    - app/views/sessions/new.html.erb
        - &lt;%= form_for :session, url: login_path do |f| %&gt;
            - &lt;%= f.email_field :email, placeholder: 'Email' %&gt;
            - &lt;%= f.password_field :password, placeholder: 'Password' %&gt;
            - &lt;%= f.submit 'Log in'%&gt;

        - &lt;% end %&gt;

    - app/controllers/sessions_controller.rb
        - def create
            - @user = User.find_by(email: params[:session][:email])
            - if @user && @user.authenticate(params[:session][:password])
                - redirect_to '/'

            - else
                - render 'new'

            - end

        - end

- 로그아웃
    - config/routes.rb
        - delete '/logout' =&gt; 'sessions#destroy'

    - app/controllers/sessions_controller.rb
        - def destroy
            - session[:user_id] = nil
            - redirect_to '/'

        - end

- 모든 페이지에서 로그인 체크
    - app/controllers/application_controller.rb
        - helper_method :current_user # 뷰에서도 표시한 메소드에 접근할 수 있게 해준다.
        - def current_user
            - @user = User.find(session[:user_id]) if session[:user_id]

        - end
        - def require_user
            - redirect_to '/login' unless current_user

        - end

    - app/controller/albums_controller.rb
        - before_action :require_user, only: [:index, :show]

    - app/views/layouts/application.html.erb
        - &lt;% if current_user %&gt;
            - &lt;ul&gt;
                - &lt;li&gt;&lt;%= current_user.email %&gt;&lt;/li&gt;
                - &lt;li&gt;&lt;%= link_to 'Log out', logout_path, method: 'delete' %&gt;&lt;/li&gt;

            - &lt;/ul&gt;

        - &lt;% else %&gt;
            - &lt;ul&gt;
                - &lt;li&gt;&lt;%= link_to 'Log in', login_path %&gt;&lt;/li&gt;
                - &lt;li&gt;&lt;%= link_to 'Signup', '/signup' %&gt;&lt;/li&gt;

            - &lt;/ul&gt;

        - &lt;% end %&gt;

- 역할 기반 인증 시스템
    - $ rails g migration AddRoleToUsers role:string
    - $ rake db:migrate
    - app/models/users.db
        - def editor?
            - self.role == 'editor'

        - end

    - app/controllers/recipes_controller.rb
        - before_action :require_editor, only: [:show, :edit]

    - app/views/recipes/show.html
        - &lt;% if current_uder && current_user.editor? %&gt;
            - &lt;%= link_to 'Edit Recipe', edit_recipe_path(@recipe.id) %&gt;

        - &lt;% end %&gt;
