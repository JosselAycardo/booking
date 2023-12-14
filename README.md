<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="book.css">
    <title>Booking</title>
</head>
<body>
    <div class="background">
        <div class="booking-form">
            <h2>Dental Booking</h2>
            <form action="booking.php" method="post">
                <label for="name">Name:</label>
                <input type="text" name="name" id="name" required>
                <label for="email">Email:</label>
                <input type="text" name="email" id="email" required>
                <label for="time">Time:</label>
                <input type="time" name="time" id="time" required>
                <label for="clinic">Clinic:</label>
                <input type="text" name="clinic" id="clinic" required>
                <label for="date">Date:</label>
                <input type="date" name="date" id="date" required>
                <label for="concern">Concern:</label>
                <input type="text" name="concern" id="concern" required>
                <button type="submit">Submit</button>
            </form>
        </div>
    </div>
    
</body>
</html>



php
<?php

$servername = "localhost";
$username = "root";
$password = "";
$dbanme = "booking";
$conn = new mysqli($servername,$username,$password,$dbanme);

if($conn->connect_error){
    die("Connection Failed:" .$conn->connect_error);

}
//Handle form submission
if($_SERVER["REQUEST_METHOD"] == "POST"){
    $name = $_POST["name"];
    $email = $_POST["email"];
    $time = $_POST["time"];
    $date = $_POST["date"];
    $clinic = $_POST["clinic"];
    $concern = $_POST["concern"];

    //prepare and execute the database insertion
    $sql = "INSERT INTO `booking`(`name`, `email`, `time`, `date`, `clinic`,`concern`)
     VALUES ('$name','$email','$time','$date','$clinic','$concern')";

     if($conn->query($sql) == TRUE){
        echo "<div class='message'
            <p>Booking Successfully</p>
            </div> <br>";
        echo "<a href='Example.html'> <button class ='btn'>Go Back</button>";
     }else{
        echo "Error: " .$sql . "<br>" .$conn->error; 
     }
}
$conn->close();
?>





css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500&display=swap');
body,html{
    padding: 0;
    height: 100%;
    margin: 0;
    font-family: 'poppins',sans-serif;
}
.container{
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 90vh;
}
.background{
    background-image: url('clinic1.jpg');
    background-size: cover;
    background-position: center;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    backdrop-filter: blur(50px);
}
.booking-form{
    background-color: rgba(255,255,255,0.7);
    padding: 20px;
    border-radius: 10px;
    max-width: 500px;
    width: 80%;
    margin: 0 auto;
    min-height: 200px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.349);
}
.booking-form h2{
    text-align: center;
}
.booking-form form{
    display: flex;
    flex-direction: column;
}
.booking-form select {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 5px;
}
.booking-form input{
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 5px;
}
.booking-form button{
    margin-top:10px;
    padding: 10px;
    background: rgba(76,68,182,0.808);
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
.booking-form button:hover{
    background: rgba(112, 106, 238, 0.808);
}
.message {
    text-align: center;
    background: #f9eded;
    padding: 15px 0px;
    border: 1px solid #699053;
    border-radius: 5px;
    margin-bottom: 10px;
    color: red;
    position: relative;
    right: 0;
    margin: auto;
}
