# IT314 : Lab 8 - Python Unit Testing

### Group : 19

## Employee Class
```
class Employee(models.Model):
    employeeID = models.CharField(max_length=10, primary_key=True)
    name = models.CharField(max_length=64)
    email = models.EmailField()
    joiningDate = models.DateField(null=True, blank=True)
    salary = models.PositiveIntegerField(default=0)
    role = models.CharField(max_length=6, default='E',
        choices=[
            ("PM", "Project Manager"),
            ("RM", "Resource Manager"),
            ("E", "Employee"),
        ])

    def __str__(self):
        return self.employeeID
    
    def getBonus(self):
        if self.role == 'PM':
            return (self.salary)*0.15;
        else:
            return (self.salary)*0.10;

```


## EmployeeTest 

`elon`, `tim` and `anil` are decalred as Employee objects in the `setUp()` method of `EmployeeTestCase` class. These objects are saved in a temporary test database which is deleted after test runs successfully. We are testing the `getBonus()` method of `Employee` class which return 15% of salary for Project Managers and 10% for other employees.

```
class EmployeeTestCase(TestCase):
    def setUp(self):
        elon = Employee.objects.create(employeeID='001', name='Elon Musk', email='elon@musk.com', salary=100000, role='PM')
        tim = Employee.objects.create(employeeID='002', name='Tim Cook', email='tim@cook.com', salary=90000, role='E')
        anil = Employee.objects.create(employeeID='003', name='Anil Ambani', email='anil@ambani.com', salary=70000, role='RM')


    def testEmployeeBonus(self):
        elon = Employee.objects.get(employeeID='001')
        tim = Employee.objects.get(employeeID='002')
        anil = Employee.objects.get(employeeID='003')
        self.assertEqual(elon.getBonus(), 15000)
        self.assertEqual(tim.getBonus(), 9000)
        self.assertEqual(anil.getBonus(), 7000)
```

On running the above test we get an OK in output. All possibilities are tested in the testcase.

![image](https://user-images.githubusercontent.com/124247859/233441579-0c960db9-248a-4f99-9400-2de4211026b1.png)
