
Individual Assessment Coversheet
To be attached to the front of the assessment.

Campus:			 Bedfordview campus		 Faculty:			 Information Technology		 Module Code:			ITPCA		  Group:		1		  Lecturer’s Name:		 Mr Mosingathi	 Student Full Name: Ubaidullah Abdula	  Student Number:	Eduv4957588		 

Indicate
Yes
No
Plagiarism report attached


Declaration:
I declare that this assessment is my own original work except for source material explicitly acknowledged. I also declare that this assessment or any other of my original work related to it has not been previously, or is not being simultaneously, submitted for this or any other course. I am aware of the AI policy and acknowledge that I have not used any AI technology to generate or manipulate data, other than as permitted by the assessment instructions. I also declare that I am aware of the Institution’s policy and regulations on honesty in academic work as set out in the Conditions of Enrolment, and of the disciplinary guidelines applicable to breaches of such policy and regulations.

Signature
Date

Lecturer’s Comments:


Marks Awarded:
%


Signature
Date

1
1

Eduvos (Pty) Ltd. (formerly Pearson Institute of Higher Education) is registered with the Department of Higher Education and Training as a private higher education institution under the Higher Education Act, 101, of 1997. Registration Certificate number: 2001/HE07/008

Contents
Question 1	3
Question 2	8
Using Visual Studio, I have created a database with a connection established from Microsoft SQL Server through means of Server Explorer on Visual Studio. The server name is UABDULA in which the database is hosted. I
named the database FluffyBakes.	8
I had then proceeded to continue with the UI phase of the project in which I has set up the labels, buttons and textboxes for the relevant actions required to be actioned as per the given instructions for Fluffy Bakes.	9
I then proceeded with the required CRUD operations required which is detailed within this code below. This code also includes the required Data Validation and Error Handling required that prevents invalid inputs during product registration, customer information updates, and other processing. It also displays appropriate error
messages to users.	14
Question 3	20
	-	20
	-	20
	-	20
	-	20
	-	20

Question 1
using System;
using System.Collections.Generic;
namespace GRandStayHotel
{
class Room
{
public int RoomNumber { get; set; } public string RoomType { get; set; }
public Room(int roomNumber, string roomType)
{
roomNumber = roomNumber; roomType = roomType;
}
}
class Reservation
{
public string GuestName { get; set; } public int RoomNumber { get; set; } public DateTime CheckInDate { get; set; }
public DateTime CheckOutDate { get; set; }
public Reservation(string guestName, int roomNumber, DateTime checkIn, DateTime checkOut)
{
GuestName = guestName; RoomNumber = roomNumber; CheckInDate = checkIn; CheckOutDate = checkOut;
}
}
class HotelManagementSystem
{
private List<Room> rooms;
private List<Reservation> reservations;
public HotelManagementSystem()
{
rooms = new List<Room>
{
new Room(101, "Single"), new Room(102, "Single"), new Room(201, "Double"), new Room(202, "Double"),

new Room(301, "Suite"),
};
reservations = new List<Reservation>();
}
private bool IsRoomAvailableForDates(int roomNumber, DateTime checkIn, DateTime checkOut)
{
for (int idx = 0; idx < reservations.Count; idx++)
{
Reservation reservation = reservations[idx];
if (reservation.RoomNumber == roomNumber)
{
//We need to check to see if there is a date overlap
if (checkIn < reservation.CheckOutDate && checkOut > reservation.CheckInDate)
{
return false; // Case in which an overlap is found
}
}
}
return true; // Case in which an overlap is not found

}

public void BookRoom()
{
Console.WriteLine(/* Output */ "Enter Guest Name: "); string guestName = Console.ReadLine();
Console.WriteLine(/* Output */ "Enter Room Type (Single/Double/Suite): "); string roomType = Console.ReadLine(); Console.WriteLine(/* Output */ "Enter in Check-in Date (MM/DD/YYYY): "); DateTime checkIn = DateTime.Parse(Console.ReadLine()); DateTime checkOut = DateTime.Parse(Console.ReadLine());

Room availableRoom = null;
for (int idx = 0; idx < rooms.Count; idx++)
{
Room room = rooms[idx];
if (room.RoomType == roomType && IsRoomAvailableForDates(room.RoomNumber, checkIn, checkOut))
{
availableRoom = room; break;
}
}

if (availableRoom != null)
{
reservations.Add(new Reservation(guestName, availableRoom.RoomNumber, checkIn, checkOut)); Console.WriteLine(/* Output */ $"Room {availableRoom.RoomNumber} booked for {guestName} from {checkIn:MM/dd/yyyy} to
{checkOut:MM/dd/yyyy}.");

}
else
{

Console.WriteLine(/* Output */ "No available rooms of this type.");
}
}

public void CheckInGuest()
{
Console.WriteLine(/* Output */ "Enter Guest Name: "); string guestName = Console.ReadLine(); Console.WriteLine(/* Output */ "Enter Room Number: ");
int roomNumber = int.Parse(Console.ReadLine());

bool found = false;
for (int idx = 0; idx < reservations.Count; idx++)
{
Reservation reservation = reservations[idx];
if (reservation.RoomNumber == roomNumber && reservation.GuestName == guestName)
{
Console.WriteLine(/* Output */ $"{guestName} has been checked into room {roomNumber}."); found = true;
break;
}
}

if (!found)
{
Console.WriteLine(/* Output */ "No matching reservation found.");

}
}

public void CheckOutGuest()
{
Console.WriteLine(/* Output */ "Enter Room Number to check-out:"); int roomNumber = int.Parse(Console.ReadLine());

int reservationIndex = -1;
for (int idx = 0; idx < reservations.Count; idx++)
{
if (reservations[idx].RoomNumber == roomNumber)
{
reservationIndex = i; break;
}
}

if (reservationIndex != -1)
{
reservations.RemoveAt(reservationIndex);
Console.WriteLine(/* Output */ $"Room {roomNumber} is now available for new guests. ");
}
else
{
Console.WriteLine(/* Output */ "Room not found or no active reservation. ");

}

}

public void ViewAvailableRooms()
{
Console.WriteLine(/* Output */ "Enter Check-in Date (MM/DD/YYYY): "); DateTime checkIn = DateTime.Parse(Console.ReadLine()); Console.WriteLine(/* Output */ "Enter Check-out Date (MM/DD/YYYY)"); DateTime checkOut = DateTime.Parse(Console.ReadLine());

Console.WriteLine(/* Output */ "Available Rooms: "); for (int idx = 0; idx < rooms.Count; idx++)
{
Room room = rooms[idx];
if (IsRoomAvailableForDates(room.RoomNumber, checkIn, checkOut))
{
Console.WriteLine(/* Output */ $"Room {room.RoomNumber} ({room.RoomType})");
}
}
}

public void ViewReservationHistory()
{
Console.WriteLine(/* Output */ "Reservation History:"); for (int idx = 0; idx < reservations.Count; idx++)
{
Reservation r = reservations[idx];
Console.WriteLine(/* Output */ $"Room {r.RoomNumber}, Guest: {r.GuestName}, From: {r.CheckInDate} To:
{r.CheckOutDate:MM/dd/yyyy}");

}
}

public void Run()
{
while (true)
{
Console.WriteLine(/* Output */ "1. Book Room"); Console.WriteLine(/* Output */ "2. Check-in Guest"); Console.WriteLine(/* Output */ "3. Check-out Guest"); Console.WriteLine(/* Output */ "4. View Available Rooms"); Console.WriteLine(/* Output */ "5. View Reservation History"); Console.WriteLine(/* Output */ "6.Exit"); Console.WriteLine(/* Output */ "Choose an option:");

string choice = Console.ReadLine();

switch (choice)
{
case "1": BookRoom(); break;

case "2": CheckInGuest(); break;
case "3": CheckOutGuest(); break;
case "4": BookRoom(); break;
case "5": ViewAvailableRooms(); break;
case "6": return;
default:
Console.WriteLine(/* Output */ "Invalid choice. Please try again."); break;
}
}
}
}
class MainProgram
{
static void Main(string[] args)
{
HotelManagementSystem hotel = new HotelManagementSystem(); hotel.Run();

}
}
}
case "2": CheckInGuest(); break;
case "3": CheckOutGuest(); break;
case "4": BookRoom(); break;
case "5": ViewAvailableRooms(); break;
case "6": return;
default:
Console.WriteLine(/* Output */ "Invalid choice. Please try again."); break;
}
}
}
}
class MainProgram
{
static void Main(string[] args)
{
HotelManagementSystem hotel = new HotelManagementSystem(); hotel.Run();

}
}
}

Question 2

Using Visual Studio, I have created a database with a connection established from Microsoft SQL Server through means of Server Explorer on Visual Studio. The server name is UABDULA in which the database is hosted. I named the database FluffyBakes.

I then created tables using a SQL query as per the preceding photo


I had then proceeded to continue with the UI phase of the project in which I has set up the labels, buttons and textboxes for the relevant actions required to be actioned as per the given instructions for Fluffy Bakes.
The code for this design can be seen below.
using System; using System.Data;
using System.Data.SqlClient; using System.Windows.Forms; using System.Configuration;

namespace BakeryManagementSystem
{
partial class ProductManagementForm
{
/// <summary>
/// Required designer variable.
/// </summary>
private System.ComponentModel.IContainer components = null;

/// <summary>
/// Clean up any resources being used.
/// </summary>
/// <param name="disposing">true if managed resources should be disposed; otherwise, false.</param>
protected override void Dispose(bool disposing)
{
if (disposing && (components != null))
{
components.Dispose();
}
base.Dispose(disposing);
using System; using System.Data;
using System.Data.SqlClient; using System.Windows.Forms; using System.Configuration;

namespace BakeryManagementSystem
{
partial class ProductManagementForm
{
/// <summary>
/// Required designer variable.
/// </summary>
private System.ComponentModel.IContainer components = null;

/// <summary>
/// Clean up any resources being used.
/// </summary>
/// <param name="disposing">true if managed resources should be disposed; otherwise, false.</param>
protected override void Dispose(bool disposing)
{
if (disposing && (components != null))
{
components.Dispose();
}
base.Dispose(disposing);

}

#region Windows Form Designer generated code

/// <summary>
/// Required method for Designer support - do not modify
/// the contents of this method with the code editor.
/// </summary>
private void InitializeComponent()
{
lblProductID = new Label(); lblProductName = new Label(); lblCategory = new Label(); lblPrice = new Label(); lblQuantityInStock = new Label(); txtProductID = new TextBox(); txtProductName = new TextBox(); txtCategory = new TextBox(); txtPrice = new TextBox(); txtQuantityInStock = new TextBox(); button1 = new Button();
button2 = new Button(); button3 = new Button(); button4 = new Button();
dataGridViewProducts = new DataGridView(); ((System.ComponentModel.ISupportInitialize)dataGridViewProducts).BeginInit()
;
SuspendLayout();
//
// lblProductID
//
lblProductID.AutoSize = true; lblProductID.BackColor = SystemColors.Control;
lblProductID.ForeColor = SystemColors.ActiveCaptionText; lblProductID.Location = new Point(86, 63); lblProductID.Name = "lblProductID";
lblProductID.Size = new Size(79, 20); lblProductID.TabIndex = 0; lblProductID.Text = "Product ID";
//
// lblProductName
//
lblProductName.AutoSize = true; lblProductName.Location = new Point(61, 109); lblProductName.Name = "lblProductName"; lblProductName.Size = new Size(104, 20); lblProductName.TabIndex = 1; lblProductName.Text = "Product Name";
//
// lblCategory

//
lblCategory.AutoSize = true; lblCategory.Location = new Point(96, 162); lblCategory.Name = "lblCategory"; lblCategory.Size = new Size(69, 20); lblCategory.TabIndex = 2; lblCategory.Text = "Category";
//
// lblPrice
//
lblPrice.AutoSize = true; lblPrice.Location = new Point(124, 211); lblPrice.Name = "lblPrice"; lblPrice.Size = new Size(41, 20); lblPrice.TabIndex = 3;
lblPrice.Text = "Price";
//
// lblQuantityInStock
//
lblQuantityInStock.AutoSize = true; lblQuantityInStock.Location = new Point(44, 268); lblQuantityInStock.Name = "lblQuantityInStock"; lblQuantityInStock.Size = new Size(121, 20); lblQuantityInStock.TabIndex = 4; lblQuantityInStock.Text = "Quantity in Stock";
//
// txtProductID
//
txtProductID.AcceptsReturn = true; txtProductID.Location = new Point(181, 63); txtProductID.Name = "txtProductID"; txtProductID.ReadOnly = true; txtProductID.Size = new Size(125, 27); txtProductID.TabIndex = 5;
//
// txtProductName
//
txtProductName.Location = new Point(181, 109); txtProductName.Name = "txtProductName"; txtProductName.Size = new Size(125, 27); txtProductName.TabIndex = 6;
//
// txtCategory
//
txtCategory.Location = new Point(181, 162); txtCategory.Name = "txtCategory"; txtCategory.Size = new Size(125, 27); txtCategory.TabIndex = 7;
//
// txtPrice

//
txtPrice.Location = new Point(181, 211); txtPrice.Name = "txtPrice"; txtPrice.Size = new Size(125, 27); txtPrice.TabIndex = 8;
//
// txtQuantityInStock
//
txtQuantityInStock.Location = new Point(181, 265); txtQuantityInStock.Name = "txtQuantityInStock"; txtQuantityInStock.Size = new Size(125, 27); txtQuantityInStock.TabIndex = 9;
//
// button1
//
button1.Location = new Point(86, 378); button1.Name = "button1"; button1.Size = new Size(94, 29); button1.TabIndex = 10;
button1.Text = "Add Product"; button1.UseVisualStyleBackColor = true; button1.Click += button1_Click;
//
// button2
//
button2.Location = new Point(220, 378); button2.Name = "button2";
button2.Size = new Size(94, 29); button2.TabIndex = 11; button2.Text = "Update Product";
button2.UseVisualStyleBackColor = true; button2.Click += button2_Click;
//
// button3
//
button3.Location = new Point(354, 378); button3.Name = "button3";
button3.Size = new Size(94, 29); button3.TabIndex = 12; button3.Text = "Delete Product";
button3.UseVisualStyleBackColor = true; button3.Click += button3_Click;
//
// button4
//
button4.Location = new Point(494, 378); button4.Name = "button4";
button4.Size = new Size(94, 29); button4.TabIndex = 13; button4.Text = "Clear Fields";

button4.UseVisualStyleBackColor = true; button4.Click += button4_Click;
//
// dataGridViewProducts
// dataGridViewProducts.ColumnHeadersHeightSizeMode =
DataGridViewColumnHeadersHeightSizeMode.AutoSize; dataGridViewProducts.Location = new Point(401, 63); dataGridViewProducts.Name = "dataGridViewProducts"; dataGridViewProducts.ReadOnly = true; dataGridViewProducts.RowHeadersWidth = 51; dataGridViewProducts.Size = new Size(300, 188); dataGridViewProducts.TabIndex = 14; dataGridViewProducts.SelectionChanged +=
dataGridViewProducts_SelectionChanged_1;
//
// ProductManagementForm
//
AutoScaleDimensions = new SizeF(8F, 20F); AutoScaleMode = AutoScaleMode.Font; ClientSize = new Size(800, 450); Controls.Add(dataGridViewProducts); Controls.Add(button4); Controls.Add(button3); Controls.Add(button2); Controls.Add(button1); Controls.Add(txtQuantityInStock); Controls.Add(txtPrice); Controls.Add(txtCategory); Controls.Add(txtProductName); Controls.Add(txtProductID); Controls.Add(lblQuantityInStock); Controls.Add(lblPrice); Controls.Add(lblCategory); Controls.Add(lblProductName); Controls.Add(lblProductID);
Name = "ProductManagementForm"; Text = "Form1";
((System.ComponentModel.ISupportInitialize)dataGridViewProducts).EndInit(); ResumeLayout(false);
PerformLayout();
}

#endregion

private Label lblProductID; private Label lblProductName; private Label lblCategory; private Label lblPrice;
private Label lblQuantityInStock;

private TextBox txtProductID; private TextBox txtProductName; private TextBox txtCategory; private TextBox txtPrice;
private TextBox txtQuantityInStock; private Button button1;
private Button button2; private Button button3; private Button button4;
private DataGridView dataGridViewProducts;
}
}
private TextBox txtProductID; private TextBox txtProductName; private TextBox txtCategory; private TextBox txtPrice;
private TextBox txtQuantityInStock; private Button button1;
private Button button2; private Button button3; private Button button4;
private DataGridView dataGridViewProducts;
}
}
using System; using System.Data;
using System.Data.SqlClient; using System.Windows.Forms; using System.Configuration;

namespace BakeryManagementSystem
{
public partial class ProductManagementForm : Form
{
private string connectionString = ConfigurationManager.ConnectionStrings["BakeryDBConnection"].ConnectionString;

public ProductManagementForm()
{
InitializeComponent(); LoadProducts();

}

private void LoadProducts()
{
using (SqlConnection conn = new SqlConnection(connectionString))
{
try
{
conn.Open();
SqlDataAdapter da = new SqlDataAdapter("SELECT * FROM Products",
conn);
DataTable dt = new DataTable(); da.Fill(dt); dataGridViewProducts.DataSource = dt;
using System; using System.Data;
using System.Data.SqlClient; using System.Windows.Forms; using System.Configuration;

namespace BakeryManagementSystem
{
public partial class ProductManagementForm : Form
{
private string connectionString = ConfigurationManager.ConnectionStrings["BakeryDBConnection"].ConnectionString;

public ProductManagementForm()
{
InitializeComponent(); LoadProducts();

}

private void LoadProducts()
{
using (SqlConnection conn = new SqlConnection(connectionString))
{
try
{
conn.Open();
SqlDataAdapter da = new SqlDataAdapter("SELECT * FROM Products",
conn);
DataTable dt = new DataTable(); da.Fill(dt); dataGridViewProducts.DataSource = dt;

}
catch (SqlException ex)
{
MessageBox.Show("Database error: " + ex.Message);
}
catch (Exception ex)
{
MessageBox.Show("Error: " + ex.Message);
}
}
}

// Add
private void btnAdd_Click(object sender, EventArgs e)
{
if (string.IsNullOrWhiteSpace(txtProductName.Text) || string.IsNullOrWhiteSpace(txtPrice.Text))
{
MessageBox.Show("Product Name and Price are mandatory."); return;
}

decimal price;
if (!decimal.TryParse(txtPrice.Text, out price) || price <= 0)
{
MessageBox.Show("Invalid Price. Price must be a positive number."); return;
}

int quantity;
if (!int.TryParse(txtQuantityInStock.Text, out quantity) || quantity < 0)
{


negative.");

}
 MessageBox.Show("Invalid Quantity. Quantity in stock cannot be return;


using (SqlConnection conn = new SqlConnection(connectionString))
{

try
{
 

conn.Open();
SqlCommand cmd = new SqlCommand("SELECT COUNT(*) FROM Products WHERE

ProductName = @ProductName", conn);
cmd.Parameters.AddWithValue("@ProductName", txtProductName.Text); int count = (int)cmd.ExecuteScalar();
if (count > 0)
{
MessageBox.Show("Product Name already exists."); return;

}

cmd = new SqlCommand("INSERT INTO Products (ProductName, Category, Price, QuantityInStock) VALUES (@ProductName, @Category, @Price, @QuantityInStock)", conn);
cmd.Parameters.AddWithValue("@ProductName", txtProductName.Text); cmd.Parameters.AddWithValue("@Category",
string.IsNullOrWhiteSpace(txtCategory.Text) ? (object)DBNull.Value : txtCategory.Text); cmd.Parameters.AddWithValue("@Price", price); cmd.Parameters.AddWithValue("@QuantityInStock", quantity); cmd.ExecuteNonQuery();
MessageBox.Show("Product added successfully."); LoadProducts();
ClearFields();
}
catch (SqlException ex)
{
MessageBox.Show("Database error: " + ex.Message);
}
catch (Exception ex)
{
MessageBox.Show("Error: " + ex.Message);
}
}
}

// Update
private void btnUpdate_Click(object sender, EventArgs e)
{
if (string.IsNullOrWhiteSpace(txtProductID.Text))
{
MessageBox.Show("Please select a product to update."); return;
}

int productID;
if (!int.TryParse(txtProductID.Text, out productID))
{
MessageBox.Show("Invalid Product ID."); return;
}

if (string.IsNullOrWhiteSpace(txtProductName.Text) || string.IsNullOrWhiteSpace(txtPrice.Text))
{
MessageBox.Show("Product Name and Price are mandatory."); return;
}

decimal price;

if (!decimal.TryParse(txtPrice.Text, out price) || price <= 0)
{
MessageBox.Show("Invalid Price. Price must be a positive number."); return;
}

int quantity;
if (!int.TryParse(txtQuantityInStock.Text, out quantity) || quantity < 0)
{
MessageBox.Show("Invalid Quantity. Quantity in stock cannot be
negative.");
return;
}

using (SqlConnection conn = new SqlConnection(connectionString))
{
try
{
conn.Open();
SqlCommand cmd = new SqlCommand("SELECT COUNT(*) FROM Products WHERE
ProductName = @ProductName AND ProductID != @ProductID", conn);
cmd.Parameters.AddWithValue("@ProductName", txtProductName.Text); cmd.Parameters.AddWithValue("@ProductID", productID);
int count = (int)cmd.ExecuteScalar(); if (count > 0)
{


exists.");
 MessageBox.Show("Another product with this name already

return;
}


cmd = new SqlCommand("UPDATE Products SET ProductName = @ProductName, Category = @Category, Price = @Price, QuantityInStock = @QuantityInStock WHERE ProductID = @ProductID", conn);
cmd.Parameters.AddWithValue("@ProductName", txtProductName.Text); cmd.Parameters.AddWithValue("@Category",
string.IsNullOrWhiteSpace(txtCategory.Text) ? (object)DBNull.Value : txtCategory.Text); cmd.Parameters.AddWithValue("@Price", price); cmd.Parameters.AddWithValue("@QuantityInStock", quantity); cmd.Parameters.AddWithValue("@ProductID", productID); cmd.ExecuteNonQuery();
MessageBox.Show("Product updated successfully."); LoadProducts();
ClearFields();
}
catch (SqlException ex)
{
MessageBox.Show("Database error: " + ex.Message);
}
catch (Exception ex)

{
MessageBox.Show("Error: " + ex.Message);
}
}
}

// Delete
private void btnDelete_Click(object sender, EventArgs e)
{
if (string.IsNullOrWhiteSpace(txtProductID.Text))
{
MessageBox.Show("Please select a product to delete."); return;
}

int productID;
if (!int.TryParse(txtProductID.Text, out productID))
{
MessageBox.Show("Invalid Product ID."); return;
}

using (SqlConnection conn = new SqlConnection(connectionString))
{
try
{
conn.Open();
SqlCommand cmd = new SqlCommand("SELECT COUNT(*) FROM OrderDetails
WHERE ProductID = @ProductID", conn);
cmd.Parameters.AddWithValue("@ProductID", productID); int count = (int)cmd.ExecuteScalar();
if (count > 0)
{
MessageBox.Show("Cannot delete product because it is part of
existing orders.");
return;
}



@ProductID", conn);





}
 cmd = new SqlCommand("DELETE FROM Products WHERE ProductID =

cmd.Parameters.AddWithValue("@ProductID", productID); cmd.ExecuteNonQuery();
MessageBox.Show("Product deleted successfully."); LoadProducts();
ClearFields();

catch (SqlException ex)
{
MessageBox.Show("Database error: " + ex.Message);
}

catch (Exception ex)
{
MessageBox.Show("Error: " + ex.Message);
}
}
}

// Clear
private void btnClear_Click(object sender, EventArgs e)
{
ClearFields();
}

private void ClearFields()
{
txtProductID.Text = ""; txtProductName.Text = ""; txtCategory.Text = ""; txtPrice.Text = ""; txtQuantityInStock.Text = "";
}


private void dataGridViewProducts_SelectionChanged(object sender, EventArgs e)
{
if (dataGridViewProducts.SelectedRows.Count > 0)
{
DataGridViewRow row = dataGridViewProducts.SelectedRows[0]; txtProductID.Text = row.Cells["ProductID"].Value.ToString(); txtProductName.Text = row.Cells["ProductName"].Value.ToString(); txtCategory.Text = row.Cells["Category"].Value?.ToString() ?? ""; txtPrice.Text = row.Cells["Price"].Value.ToString(); txtQuantityInStock.Text = row.Cells["QuantityInStock"].Value.ToString();
}
}

private void button1_Click(object sender, EventArgs e)
{

}

private void button2_Click(object sender, EventArgs e)
{

}

private void button3_Click(object sender, EventArgs e)
{

}

private void button4_Click(object sender, EventArgs e)
{

}

private void dataGridViewProducts_SelectionChanged_1(object sender, EventArgs e)
{

}
}
}
private void button4_Click(object sender, EventArgs e)
{

}

private void dataGridViewProducts_SelectionChanged_1(object sender, EventArgs e)
{

}
}
}

Question 3

3.1
This is a custom exception designed to handle specific invalid order conditions and as such, it’s purpose is to
	-	Signal when an order cannot be processed due to invalid inputs
	-	Allow the system to catch these specific exceptions and display user friendly error messages
	-	To provide a more meaningful error handling compared to other more general exceptions This in turn allows for the developer to
Clearly identify and log error-related errors and handle these errors separately from other exceptions.

3.2
This is a fundamental mechanism for handling exceptions in c# and it works as I am about to describe.
-You have your Try block which contains the code that is going to throw an exception
-You then have your catch block which is the code thrown to handle the exception if one is thrown with the ability to catch specific exception types.

3.3
The purpose of a nested try-catch block whereby you have an outer catch and an inner catch is the separate a general exception (Outer try-catch) and specific exceptions relating to specific parts of the code (Inner try-catch).
This allows for more precise control over exception handling and makes sure that specific errors are handled different from general error.

3.4
The finally block in exception handling is used to specify code that must execute regardless of exception codes being thrown or not. This is hence used more for cleanup operations and ensuring that critical code does indeed run. In the Scenario of the Bakery Management System, the finally block can be used to close database connections after order processing., release locks on inventory and log completion of the operation.

3.5
The thow keyword is used to raise an exception. An example of this is throw new
InvalidOrderException("Quantity cannot be negative."); which is when you wish to create and throw a new exception instance.
It can also be used to rethrow an already caught exception. An example as per our scenario would be when you throw a custom exception like InvalidOrderExecution






Reference Page

Stack Overflow. (n.d.). What is the difference between data validation and exception handling? [online] Available at: https://stackoverflow.com/questions/26490182/what-is-the-difference-between-data-validation-and- exception-handling

dotnet-bot (2025). ValidationException Class (System.componentModel.DataAnnotations). [online] Microsoft.com. Available at: https://learn.microsoft.com/en-
us/dotnet/api/system.componentmodel.dataannotations.validationexception?view=net-9.0

Jovanović, M. (2023). Functional Error Handling in .NET With the Result Pattern. [online] www.milanjovanovic.tech. Available at: https://www.milanjovanovic.tech/blog/functional-error-handling-in-dotnet-with-the-result-pattern

Pasindu Sandamal (2024). Develop simple crud application using C# with .net framework based on SQLite database. [online] Medium. Available at: https://medium.com/@sandamalpkp318/develop-simple-crud- application-using-c-with-net-framework-based-on-sqlite-database-d33ce45cfad9
gathogojr (2022). Basic CRUD in ASP.NET Core OData 8 - OData. [online] Microsoft.com. Available at: https://learn.microsoft.com/en-us/odata/webapi-8/tutorials/basic-crud?tabs=net60%2Cvisual-studio- 2022%2Cvisual-studio%2Cvs2022

anjat99 (2021). GitHub - anjat99/Hotel_System: A simple admin panel for managing system for hotel built using C#, WindowsForms, MySQL. [online] GitHub. Available at: https://github.com/anjat99/Hotel_System

WilliamDAssafMSFT (n.d.). Design your first relational database C# - Azure SQL Database. [online]
learn.microsoft.com. Available at: https://learn.microsoft.com/en-us/azure/azure-sql/database/design-first- database-csharp-tutorial?view=azuresql
Archiveddocs (2009). InvalidOrderException Class (Microsoft.Synchronization). [online] Microsoft.com. Available at: https://learn.microsoft.com/en-us/previous-versions/sql/synchronization/sync-framework-
1.0/cc306196(v%3Dsql.100)

W3schools.com. (2025). W3Schools. [online] Available at: https://profile.w3schools.com/log- in?redirect_url=https%3A%2F%2Fwww.w3schools.com%2Fcs%2Fcs_exceptions.php

Wagner, B. (2023). Exception-handling statements - throw and try, catch, finally. [online] learn.microsoft.com. Available at: https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/exception- handling-statements
CJ7 (2010). What does ‘throw;’ by itself do? [online] Stack Overflow. Available at: https://stackoverflow.com/questions/2728640/what-does-throw-by-itself-do


