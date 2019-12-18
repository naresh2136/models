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
    
