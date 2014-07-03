# Week 4 Comprehensive Assessment

Fork this repository, update this file to include your answers, and submit a pull request. You may refer to any notes, past projects, or external resources you want. The questions do not have to be completed in order.

1. My app has Students who are organized into Houses. What lines should I add to `config/routes.rb` to create a complete set of nested RESTful routes for these resources?

resources :houses


2. Write a migration to create a `students` table with columns for name, age, and something to link the student to the `House` they belong to.

1. rails g migration CreateStudents name:text age:integer

2. Go into migration and add t.references :house, index: true to table

3. rake db:migrate

3. Assuming a Student can only be in a single House, what kind of associations should I define on these models? Do I need to introduce any new models, and if so, what associations should I define on those?

A student should belong to a house, so within the student model you would list belongs_to :house.

You should create a house model (if it doesn't already exist) and then list has_many :students in that model.

4. Now I want Students to be able to enroll in Courses. What kind of associations should I define on these models? Do I need to introduce any new models, and if so, what associations should I define on those?

Students would have many courses (has_many :courses in students model) and courses would have many students (has_many :students in courses model). If it doesn't exist already, you'd need to create the courses model.


5. I want Students to be able to leave Comments on both Courses and Professors. What kind of associations should I define on these models? Do I need to introduce any new models, and if so, what associations should I define on those?

You would have to create a professors model and I would create a polymorphic relationship of 'commentable'. Both professors and courses would each have many comments as commentable. Comments would belong to students and commentable.


6. When creating a new Student in my students controller, assuming I have a `student_params` method and the house the student should belong to is stored in `@house`, what code should I write to link the student to the house?


7. If I'm using Devise with a User model, what code should I write in a controller or view to find out whether a user is signed in? And how can I get a reference to the currently-signed-in user?


8. If I'm using Devise with a User model, what code should I write in my students controller so that only signed-in users can access the `new` and `create` actions?

before_action :authenticate_user!, only: [:new, :create]

9. When I deploy a new version of my app to Heroku that contains a new migration, how can I run that migration on my production database?


10. If accessing my app on Heroku gives me an uninformative "something went wrong" error message, how can I find out what the real error is?

heroku apps:info --app <app_name>
