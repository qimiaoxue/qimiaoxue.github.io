---
layout: post
title:  XlsxWriter 
date:   2017-05-18 10:30:52 +0800
categories: python excel 
tag: excel 
---

* content
{:toc}


### xlsxwriter reference 
```
http://xlsxwriter.readthedocs.io/
```

### install xlsxwriter 
```
$ sudo pip install XlsxWriter 
```
### xlsxwriter instance 
```
$ workbook = xlsxwriter.Workbook(filenama)
$ worsheet = workbook.add_worksheet() 
```
### use worksheet 
```
$ row = 0 
$ col = 0 
$ worksheet.write(row, col, 'HelloWorld') 
```
### set xlsxwriter column width
```
$ worksheet.set_column('A:E', 14)
```
### case_1 
```
expenses = (
    ['Rent', 1000],
    ['Gas',   100],
    ['Food',  300],
    ['Gym',    50],
)
row = 0 
col = 0 
for item, cost in (expenses):
    worksheet.write(row, col,     item)
    worksheet.write(row, col + 1, cost)
    row += 1
worksheet.write(row, 0, 'Total')
worksheet.write(row, 1, '=SUM(B1:B4)')
workbook.close() 
```
### case_2  
```
def get_xlsx(filename, array):
    workbook = xlsxwriter.Workbook(filename)
    worksheet = workbook.add_worksheet()
    worksheet.write(0, 0, 'enrollemnt.unique')
    row = 1
    col = 0
    for i, e in enumerate(array):
        for j, f in enumerate(e):
            worksheet.write(row + j, col + i, f)
    workbook.close()


if __name__ == '__main__':
    expenses = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    filename = 'tutorial03.xlsx'
    get_xlsx(filename, expenses)
```

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
