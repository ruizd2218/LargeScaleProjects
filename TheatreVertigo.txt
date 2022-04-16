In this project, I helped create a Blog section of the website for a local theater. This blog section allowed a user to upload an image to the database, then they would 
be able to see that image and any other images shared by anybody else, it also allowed them to edit and delete the images if needed. 

I also added a very similar section but meant for specific authors at the theater, you could add an author's name, bio, and date joined, as well as the date they left, 
then it would be stored in a database. I also handled the styling of these pages. This project strengthened my C# and .NET skills exponentially. 
I thoroughly enjoyed this project and the learning experience it gave me.

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
