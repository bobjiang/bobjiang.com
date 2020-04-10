---
title: "Ruby On Rails 学习笔记（2）"
date: "2013-12-17"
---

上一次说到如何在windows下快速搭建学习环境，以及ruby on rails的项目目录结构 可以参考：[http://bobjiang.com/2013/12/11/ruby-on-rails/](http://bobjiang.com/2013/12/11/ruby-on-rails/)

本次的学习目标是CRUD（Create, Read, Update, Destroy）中的C和R

- **如何创建记录**

1\. 打开文件config/routes.rb文件，添加一行代码：

`resources :books`

这行的含义是映射对于/books的http请求，下面会介绍细节 2. 从开始菜单打开“Commands Prompt with Ruby and Rails”，然后执行命令

`rake routes`

将会显示出对于/books的路由规则

`books GET /books(.:format) books#index POST /books(.:format) books#create new_book GET /books/new(.:format) books#new edit_book GET /books/:id/edit(.:format) books#edit book GET /books/:id(.:format) books#show PUT /books/:id(.:format) books#update DELETE /books/:id(.:format) books#destroy`

_备注：路由规则，就是对于不同的url请求，路由到controller不同的方法。比如上面的例子中/books get方法路由到books controller的index方法，而/books post方法路由到books controller create方法，以此类推。_

3\. 下面我们从controller开始，controller是MVC的核心部分，控制请求的处理和转发。 假设当前rails server是运行状态，在浏览器地址栏输入http://localhost:3000/books/new 将会提示controller未初始化。因此创建controller

`rails g controller books`

继续刷新网页http://localhost:3000/books/new 得到新错误，BooksController中没有new方法。 然后打开创建的controller，（app/controller/books\_controller.rb）定义new方法

`def new end`

再刷新，新的错误，提示没有template，即没有对应的viewer。 4. 新建文件 app/views/books/new.html.erb 文件内容为"New Book"

> <h1>New Book</h1> <%= form\_for :book, url: books\_path do |f| %>
> 
> <p> <%= f.label :name %><br /> <%= f.text\_field :name %> </p> <p> <%= f.label :description %><br /> <%= f.text\_area :description %> </p>
> 
> <p> <%= f.submit %> </p> <% end %>

- **显示单条记录**

5\. 刷新网页，输入书名和描述，点击提交，提示错误，没有create action。返回books controller，添加create方法

`def create reder text: params[:book].inspect end`

6\. 再次提交，成功。 至此，我们完成了一条记录的创建，和回显当前成功的这条记录。

**本节的要点总结**: controller是控制http请求和转发的核心（用rails g controller命令创建）。viewer是显示层，直接在app/views/books/目录下手动创建对应的文件，后缀名是.html.erb
