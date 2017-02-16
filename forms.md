[可以通过widget来改变form表单的html元素](https://docs.djangoproject.com/en/1.8/topics/forms/)

[如果forms.is\_valid\(\)校验成功，数据会以字典的形式被存储到`form.cleaned_data（）中，通过form.cleaned_data[key]的形式获取数据，如果key对应de是IntegerField，那么form.cleaned_data[key]返回整数类型`](https://docs.djangoproject.com/en/1.8/topics/forms/)

[如果form的fileds是`FileField或者是ImageField，那么需要添加`enctype=“multipart/form-data”,并且，传递参数的时候，将request.POST和request.FILES同时传入](https://docs.djangoproject.com/en/1.8/ref/forms/api/#binding-uploaded-files)

[使用forms.errors的时候，可以不用is\_valid\(\)方法，forms.errors会先自动调用is valid\(\)方法的](https://docs.djangoproject.com/en/1.8/ref/forms/api/#binding-uploaded-files)

怎样自定义User mode\(https://docs.djangoproject.com/en/1.9/topics/auth/customizing/\#auth-custom-user and http://www.ziqiangxuetang.com/django/django-registration.html\)

