# wt-nafis-salman

To implement the Delete feature in MVC, you would need to follow these steps:

Step 1: Import the employee.sql file in your data via phpMyAdmin.

Step 2: Create a Model to handle the database operations. Here's an example:

```

class EmployeeModel {
    private $conn;

    public function __construct($db) {
        $this->conn = $db;
    }

    public function deleteEmployee($id) {
        $sql = "DELETE FROM employee WHERE id = :id";
        $stmt = $this->conn->prepare($sql);
        $stmt->bindParam(':id', $id, PDO::PARAM_INT);
        $stmt->execute();
    }
}
```

Step 3: Create a Controller to handle the Delete action. Here's an example:

```

class EmployeeController {
    private $model;

    public function __construct($model) {
        $this->model = $model;
    }

    public function deleteEmployee($id) {
        $this->model->deleteEmployee($id);
        header('Location: index.php');
    }
}
```
Step 4: Create a View to display the Delete form. Here's an example:

```

<form method="post" action="delete.php">
    <label for="id">Employee ID:</label>
    <input type="text" id="id" name="id">
    <input type="submit" value="Delete">
</form>
```
Step 5: Handle the form submission in a separate PHP file. Here's an example:

```
require_once 'model/EmployeeModel.php';
require_once 'controller/EmployeeController.php';

$db = new PDO('mysql:host=localhost;dbname=mydb;charset=utf8', 'username', 'password');

$model = new EmployeeModel($db);

$controller = new EmployeeController($model);

if (isset($_POST['id'])) {
    $controller->deleteEmployee($_POST['id']);
}
```

Note: Make sure to replace "mydb", "username", and "password" with your actual database name, username, and password.

Step 6: Add a link to the Delete form in your application's navigation menu.

That's it! Now you should be able to delete employees from your database using the Delete feature implemented in your MVC application.
