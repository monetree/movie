    #urls.py:
    from django.conf import settings
    from django.conf.urls.static import static
    ]+ static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)

    #settings.py:
        STATIC_URL = '/static/'
        STATICFILES_DIRS = [
          os.path.join(BASE_DIR, "static"),
        ]
        MEDIA_URL='/media/'
        MEDIA_ROOT=os.path.join(BASE_DIR, 'media')

    #upload file:
    from django.core.files.storage import FileSystemStorage
          prod_img= request.FILES['prod_img']
          fs=FileSystemStorage()
          filename=fs.save(prod_img.name,prod_img)
          url=fs.url(filename)

    #session:
          request.session['admin_id']

    #ip:
          request.META['REMOTE_ADDR']



    #database logic:
    from django.db.models import Sum,Avg,Max,Min,Count,F,Q



      context = {
      "cats":Categories.objects.all(),

      "sub_cats":SubCategories.objects.all(),

      "list_sub_cats":ListSubCategories.objects.all(),

      "data":Products.objects.values('cat_id__cat_name','prod_name','id','prod_price','prod_img','sub_cat_id__sub_cat_name','list_sub_cat_id__list_sub_cat_name'),

      "max":Products.objects.all().aggregate(Max('prod_price')),

      "min":Products.objects.all().aggregate(Min('prod_price')),

      "count":Products.objects.all().aggregate(Count('id')),

      "sum":Products.objects.all().aggregate(Sum('prod_price')),

      "prods":Products.objects.aggregate(num_prods=Count('id')),

      'groupby':Products.objects.values('prod_price').annotate(howmuch=Count('prod_price')),

      "distnict":Products.objects.values('prod_price').distinct().order_by('prod_price'),

      "or":Products.objects.filter(Q(prod_price=22000) | Q(prod_name="blackberry z10")),

      "not":Products.objects.filter(~Q(prod_price=22000)),

      'order':Products.objects.order_by('id','-prod_price'),

      'limit':Products.objects.filter(~Q(id=5))[:5],

      'between':Products.objects.filter(id__lte=25,id__gte=20),

      "in":Products.objects.filter(id__in=Products.objects.values_list(flat=True)),

      # obj21=User.objects.filter(~Q(name__icontains='soubhagya'))

      # obj25=User.objects.exclude(id__in=filter)

      # "notin":Products.objects.filter(~Q(id__in=Products.objects.values_list(flat=True))),

       "exclude":Products.objects.filter(~Q(id__in=Products.objects.filter(id=22))),

      "mtm":ModelB.objects.values('modela__a', 'b', 'modelc__c'),

      "o1":Restaurant.objects.select_related('place'),

      "o2":Waiter.objects.select_related('restaurant'),

  }
