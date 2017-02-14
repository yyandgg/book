[可以通过widget来改变form表单的html元素](https://docs.djangoproject.com/en/1.8/topics/forms/)

如果forms.is\_valid\(\)校验成功，数据会以字典的形式被存储到`form.cleaned_data（）中，通过form.cleaned_data[key]的形式获取数据，如果key对应de是IntegerField，那么form.cleaned_data[key]返回整数类型`

