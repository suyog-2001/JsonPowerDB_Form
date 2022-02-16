# JsonPowerDB_Form
<h1>Vertical (basic) form</h1>

<h3>Description</h3>
<p>I have created a form where a user can assign their Employee Id, Employee Name and their corresponding E-mail Address to the database. Where I have created one HTML file and attached javascript to it.</p>

<h4>Benifits of JsonPowerDB</h4>
<p>1. JsonPowerDB is a Deeloper Friendly API srvices.<br>
   2. JsonPowerDB is Light Weight, High Performance.<br>
   3. JsonPowerDB is Simple To use.<br>
   4. JsonPowerDB is Human Readable.<br>
   5. JsonPowerDB is Easy and fast to develop database applications without using any server side programming.
</p>


<h4>The Code I have written to make this form :</h4>


<p><!DOCTYPE html>

<html lang="en">

<head>
    <title>Bootstrap Example</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
</head>

<body>
    <div class="container">
        <h2>Vertical (basic) form</h2>
        <form id="empForm" method="post">
            <div class="form-group">
                <span><label for="empId">Employee ID:</label> <label id="empIdMsg">
                    </label></span>
                <input type="text" class="form-control" name="empId" id="empId" placeholder="Enter Employee ID"
                    required>
            </div>
            <div class="form-group">
                <label for="empName">Employee Name:</label>
                <input type="text" class="form-control" id="empName" placeholder="Enter Employee Name" name="empName">
            </div>
            <div class="form-group">
                <label for="empEmail">Email:</label>
                <input type="email" class="form-control" id="empEmail" placeholder="Enter Employee Email"
                    name="empEmail">
            </div>
            <input type="button" class="btn btn-primary" id="empSave" value="Save" onclick="saveEmployee();">
        </form>
    </div>
    <script>
        $("#empId").focus();
        function validateAndGetFormData() {
            var empIdVar = $("#empId").val();
            if (empIdVar === "") {
                alert("Employee ID Required Value");
                $("#empId").focus();
                return "";
            }
            var empNameVar = $("#empName").val();
            if (empNameVar === "") {
                alert("Employee Name is Required Value");
                $("#empName").focus();
                return "";
            }
            var empEmailVar = $("#empEmail").val();
            if (empEmailVar === "") {
                alert("Employee Email is Required Value");
                $("#empEmail").focus();
                return "";
            }
            var jsonStrObj = {
                empId: empIdVar,
                empName: empNameVar,
                empEmail: empEmailVar,
            };
            return JSON.stringify(jsonStrObj);
        }
        
        function createPUTRequest(connToken, jsonObj, dbName, relName) {
            var putRequest = "{\n"
                + "\"token\" : \""
                + connToken
                + "\","
                + "\"dbName\": \""
                + dbName
                + "\",\n" + "\"cmd\" : \"PUT\",\n"
                + "\"rel\" : \""
                + relName + "\","
                + "\"jsonStr\": \n"
                + jsonObj
                + "\n"
                + "}";
            return putRequest;
        }
        function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
            var url = dbBaseUrl + apiEndPointUrl;
            var jsonObj;
            $.post(url, reqString, function (result) {
                jsonObj = JSON.parse(result);
            }).fail(function (result) {
                var dataJsonObj = result.responseText;
                jsonObj = JSON.parse(dataJsonObj);
            });
            return jsonObj;
        }
        function resetForm() {
            $("#empId").val("")
            $("#empName").val("");
            $("#empEmail").val("");
            $("#empId").focus();
        }
        function saveEmployee() {
            var jsonStr = validateAndGetFormData();
            if (jsonStr === "") {
                return;
            }
            var putReqStr = createPUTRequest("90936861|-31948784479254024|90932362",
                jsonStr, "SAMPLE", "EMP-REL");
            alert(putReqStr);
            jQuery.ajaxSetup({ async: false });
            var resultObj = executeCommand(putReqStr,
                "http://api.login2explore.com:5577", "/api/iml");
            alert(JSON.stringify(resultObj));
            jQuery.ajaxSetup({ async: true });
            resetForm();
        }
    </script>
</body>

</html></p>