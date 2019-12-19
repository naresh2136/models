# models
from datetime import date
from django.utils import timezone

class Store(models.Model):
    name = models.CharField(max_length=30)    
    address = models.CharField(max_length=30)
    date = models.DateField(default=date.today)
    datetime = models.DateTimeField(default=timezone.now)
    date_lastupdated = models.DateField(auto_now=True)
    date_added = models.DateField(auto_now_add=True)
    timestamp_lastupdated = models.DateTimeField(auto_now=True)
    timestamp_added = models.DateTimeField(auto_now_add=True)
   
def default_city():
    return "San Diego"

class Store(models.Model):
    name = models.CharField(max_length=30)    
    address = models.CharField(max_length=30)
    city = models.CharField(max_length=30,default=default_city)
    state = models.CharField(max_length=2,default='CA')
    
 ITEM_SIZES = (
            ('S','Small'),
            ('M','Medium'),
            ('L','Large'),
            ('P','Portion'),
            )

class Menu(models.Model):
    name = models.CharField(max_length=30)

class Item(models.Model):
    menu = models.ForeignKey(Menu, on_delete=models.CASCADE)
    name = models.CharField(max_length=30)
    description = models.CharField(max_length=100)
    size = models.CharField(choices=ITEM_SIZES,max_length=1)
    

'≠================='
class Video(models.Model):
    name= models.CharField(max_length=500)
    description= models.TextField()
    videofile= models.FileField(upload_to='videos/', validators= [validate_video])

from django.shortcuts import render
from .models import Video


def showvideo(request):
 
    allvideos= Video.objects.all()
    
    context= {'allvideos': allvideos}

        
    return render(request, 'Blog/home.html', context)


html>
<head>
<meta charset="UTF-8">
<title>Videos</title>
</head>
<body>



<h1>List of Videos</h1>
<table border="1" width="600">
<tr>
<td>Name</td>
<td>Description</td>
<td>Video File</td>
</tr>

{% for video in allvideos %}
<tr>
<td>{{ video.name }}</td>
<td>
{{ video.description }}</td>
<td><video width='400' controls>
<source src='{{ MEDIA_URL }}{{ video.videofile }}' type='video/mp4'>
Your browser does not support the video tag.
</video>
</td>
</tr>
{% endfor %}
</table>
