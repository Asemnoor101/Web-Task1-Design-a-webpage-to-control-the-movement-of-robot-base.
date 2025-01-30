# Robot Base Control System 🚀

## 📌 Required Applications  
- **XAMPP** – To run PHP and MySQL.  
- **Web Browser** – To test the project.  
- **Code Editor** – VS Code or Notepad++.  

---

## 📌 What We Did?  
1. Created a **web interface** with control buttons.  
2. Set up a **MySQL database** to store movement commands.  
3. Wrote **PHP scripts** to save and retrieve commands.  

## 📌 Code  


HTML File
inside the 'index.htm', copy-paste the following code.

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="keywords" content="HTML, CSS" />
    <meta name="description" content="Controlling the movements of the robot" />
    <title>Controlling the robot movement</title>
    <link rel="stylesheet" href="styles.css" />
    <script>
      function sendMovement(direction, element) {
        var xhr = new XMLHttpRequest();
        xhr.open("POST", "send_movement.php", true);
        xhr.setRequestHeader(
          "Content-Type",
          "application/x-www-form-urlencoded"
        );
        xhr.onreadystatechange = function () {
          if (xhr.readyState === 4 && xhr.status === 200) {
            var response = JSON.parse(xhr.responseText);
            if (response.status === "success") {
              // Movement recorded successfully, do nothing
            } else {
              console.error("Error:", response.message);
            }
          }
        };
        xhr.send("direction=" + direction);

        element.classList.add("active");
        setTimeout(function () {
          element.classList.remove("active");
        }, 200);
      }
    </script>
  </head>
  <body>
    <div class="container">
      <div class="rectangle up" onclick="sendMovement('up', this)">Up</div>
      <div class="middle">
        <div class="rectangle left" onclick="sendMovement('left', this)">
          Left
        </div>
        <div class="rectangle center" onclick="sendMovement('stop', this)">
          Stop
        </div>
        <div class="rectangle right" onclick="sendMovement('right', this)">
          Right
        </div>
      </div>
      <div class="rectangle down" onclick="sendMovement('down', this)">
        Down
      </div>
    </div>
  </body>
</html>
Note

Inside the html file there is a JavaScript code between <script> </script>. it is used with HTML to create dynamic and interactive web pages.

CSS File
inside the file of "styles.css'. copy-paste the following code.

/* Your existing styles */
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}
body,
html {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative; /* Add position relative to parent */
}
.container {
    display: flex;
    flex-direction: column;
    width: 700px;
    height: 400px;
}
.rectangle {
    width: 220px;
    height: 100px;
    background-color: rgb(40, 163, 179);
    color: white;
    font-size: 20px;
    font-weight: bold;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    border-radius: 40px;
    border: 2px solid rgb(22, 117, 130);
    margin: 10px auto;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.9);
    padding: 10px;
    box-sizing: border-box;
    font-size: 40px;
    transition: transform 0.1s, background-color 0.1s;
}
.rectangle:hover,
.rectangle.active {
    transform: scale(0.95);
    background-color: rgb(30, 143, 159);
}
.up,
.down {
    height: 25%;
}
.middle {
    display: flex;
    justify-content: center;
    align-items: center;
    height: auto;
    flex: 1;
}
.left,
.center,
.right {
    flex: 1;
    margin: 0 10px;
}
.center {
    background-color: rgb(23, 42, 62);
    border: 2px solid rgb(11, 4, 63);
}
.last-movement {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 20px;
    color: rgb(40, 163, 179);
    background-color: white;
    padding: 5px 10px;
    border: 2px solid rgb(22, 117, 130);
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
}
Note

We can also insert the CSS code inside the html file between <style> </style>.

PHP file
open the folder of 'send_movement.php'. copy-paste the following code.

<?php
$servername = "localhost";
$username = "root";
$password = "";
$dbname = "robotmove";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $direction = $_POST['direction'];

    $sql = "INSERT INTO movements (direction) VALUES ('$direction')";

    if ($conn->query($sql) === TRUE) {
        echo json_encode(["status" => "success"]);
    } else {
        echo json_encode(["status" => "error", "message" => $conn->error]);
    }
}

$conn->close();
?>

📌 Project Screenshots
Web Interface:
![لقطة شاشة 2025-01-30 223040](https://github.com/user-attachments/assets/9a014e7f-3762-4a8e-bd71-419ff0bea6b6)

Database:

![لقطة شاشة 2025-01-30 223144](https://github.com/user-attachments/assets/8e5c7e4b-f007-4a52-abca-01f2c2aa627e)


سي
