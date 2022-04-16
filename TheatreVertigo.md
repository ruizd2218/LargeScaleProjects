In this project, I helped create a Blog section of the website for a local theater. This blog section allowed a user to upload an image to the database, then they would 
be able to see that image and any other images shared by anybody else, it also allowed them to edit and delete the images if needed. 

I also added a very similar section but meant for specific authors at the theater, you could add an author's name, bio, and date joined, as well as the date they left, 
then it would be stored in a database. I also handled the styling of these pages. This project strengthened my C# and MVC knowledge exponentially,
I thoroughly enjoyed this project and the learning experience it gave me.

The file upload is uploaded in the view, along with a Title for the image.
```
@using (Html.BeginForm("Create", "BlogPhotoes", FormMethod.Post, new { enctype = "multipart/form-data" }))
{
    @Html.AntiForgeryToken()

    <div class="blog-create--formContainer">
        <div class="form-horizontal">
            <hr />
            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
            <div class="form-group">
                @Html.LabelFor(model => model.Title, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Title, new { htmlAttributes = new { @class = "blog-create--inputBar", placeholder = "Enter your title here" } })
                    @Html.ValidationMessageFor(model => model.Title, "", new { @class = "text-danger" })
                </div>
            </div>

            <input type="file" name="userPhoto" value="Photo" id="userPhoto" />

            <div class="form-group blog-create--createDiv">
                <input type="submit" value="Create" class="blog-create--createBtn" />
            </div>
            <div class="blog-create--returnDiv">
                <button class="blog-create--returnBtn" onclick="location.href='@Url.Action("Index")';return false;">Back to List</button>
            </div>
        </div>
    </div>
}
```

The initial file upload converts our uploaded image to a byte, using this function
```
public byte[] ConvertToByte(HttpPostedFileBase photo)
        {
            MemoryStream memStream = new MemoryStream();
            
            photo.InputStream.CopyTo(memStream);
            byte[] bytePhoto = memStream.ToArray();
            return bytePhoto;
        }
```

This function is then called and sent to the View, where the image can then be redisplayed in the Index view where you can also see the other images that have been uploaded. It uses a foreach statement that allows it to display every entry from the database.

```
<div class="blog-index--gridContainer">
    @foreach (var item in Model)
    {
        string str = "";
        if (item.Photo != null)
        {
            str = Convert.ToBase64String(item.Photo);
        }
            
        <div class="blog-index--figure card-columns">
                    
                    
            <div id="blog-index--cardID" class="card blog-index--card">

                <p>@item.Title</p>
                <div class="blog-index--btnContainer">
                    <a href="@Url.Action("Edit", new { id = item.Id })" class="badge badge-dark blog-index--cardBtnEdit">Edit</a>
                    <a href="@Url.Action("Delete", new { id = item.Id })" class="badge badge-danger blog-index--cardBtnDlt">Delete</a>
                </div>
                <a href="@Url.Action("Details", new { id = item.Id })">
                    <img src="data:image/jpeg;base64, @str" class="card-img" alt="">
                </a>
            </div>
        </div>

    }
</div>
```

You can also edit specific entries in the edit View.

```
<div class="blog-create--formContainer">
        <div class="form-horizontal">
            <hr />
            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
            @Html.HiddenFor(model => model.Id)

            <div class="form-group">
                @Html.LabelFor(model => model.Title, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Title, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.Title, "", new { @class = "text-danger" })
                </div>
            </div>

            <div class="form-group">
                @Html.LabelFor(model => model.Photo, htmlAttributes: new { @class = "control-label col-md-2" })
                <div class="col-md-10">
                    @Html.EditorFor(model => model.Photo, new { htmlAttributes = new { @class = "form-control" } })
                    @Html.ValidationMessageFor(model => model.Photo, "", new { @class = "text-danger" })
                </div>
            </div>


            <div class="form-group home-createBPhoto--createDiv">
                <input type="submit" value="Save" class="blog-create--createBtn" />
            </div>
            <div class="home-createBPhoto--returnDiv">
                <button class="blog-create--returnBtn" onclick="location.href='@Url.Action("Index")';return false;">Back to List</button>
            </div>
        </div>
    </div>
```

The Blog authors section is not much different, allowing you to add entries of specific authors and when they joined. Here is the model in which data is stored

```
namespace TheatreCMS4.Areas.Models
{
    public class BlogAuthor
    {
        public int BlogAuthorId { get; set; }
        public string Name { get; set; }
        public string Bio { get; set; }
        public DateTime Joined { get; set; }
        public DateTime? Left { get; set; }

    }
}
```

Overall this project deeply strengthened my understanding of C# and MVC concepts. This gave me real and invaluable experience working in a codebase
and it was a great learning experience.
