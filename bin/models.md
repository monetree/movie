from django.db import models

class Categories(models.Model):
    cat_name = models.CharField(max_length=60)
    cat_status = models.BooleanField()

    def __str__(self):
        return self.cat_name


class SubCategories(models.Model):
    sub_cat_name = models.CharField(max_length=60)
    sub_cat_status = models.BooleanField()
    cat_id = models.ForeignKey(Categories,null=True)

    def __str__(self):
        return self.sub_cat_name


class ListSubCategories(models.Model):
    list_sub_cat_name = models.CharField(max_length=60)
    list_sub_cat_status = models.BooleanField()
    cat_id = models.ForeignKey(Categories,null=True)
    sub_cat_id = models.ForeignKey(SubCategories,null=True)

    def __str__(self):
        return self.list_sub_cat_name


class Products(models.Model):
    prod_name = models.CharField(max_length=60)
    prod_price = models.IntegerField(default=0)
    prod_status = models.BooleanField()
    prod_img = models.FileField(null=True,blank=True)
    cat_id = models.ForeignKey(Categories,null=True)
    sub_cat_id = models.ForeignKey(SubCategories,null=True)
    list_sub_cat_id = models.ForeignKey(ListSubCategories,null=True)



    def __str__(self):
        return self.prod_name

#ManyToManyField

class ModelA(models.Model):
    a = models.CharField(max_length=15)

class ModelC(models.Model):
    c = models.CharField(max_length=15)

class ModelB(models.Model):
    b = models.CharField(max_length=15)
    modela = models.ManyToManyField(ModelA)
    modelc = models.ManyToManyField(ModelC)

#inner join

class Place(models.Model):
    name = models.CharField(max_length=50)
    address = models.CharField(max_length=80)

class Restaurant(models.Model):
    place = models.OneToOneField(
        Place,
        on_delete=models.CASCADE,
        primary_key=True,
    )
    serves_hot_dogs = models.BooleanField(default=False)
    serves_pizza = models.BooleanField(default=False)

class Waiter(models.Model):
    restaurant = models.ForeignKey(
        Restaurant,
        on_delete=models.CASCADE
    )
    name = models.CharField(max_length=50)
