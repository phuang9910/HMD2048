<html lang="en">
<head>
<title>Bootstrap Example</title>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet"
href="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
<!-- jQuery library -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<!-- Popper JS -->
<script
src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
<!-- Latest compiled JavaScript -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>

<body>
    <div class="row">
        <BR>
    </div>
    <div class="row">
    	<div class="col-12 text-center">
            <h6> Maximum Length </h6>
            <input type="text" id="maxLength" name="maxLength" value=""><br> <br>
            <h6>Preferred Height</h6>
            <input type="text" id="preHeight" name="preHeight" value=""><br><br>
            <button type="button" id="calculate" onclick="calculate();">Calculate</button> <br> <BR> <BR>
        </div>
        <!--
        <div class="col-5 text-left">
            <h6>Lens Focus Length:</h6>
            <input type="text" id="lensFocus" name="lensFocus" value="Focus Length" disabled><br> <br>
            <h6>Installation Height:</h6>
            <input type="text" id="instHeight" name="instHeight" value="Installation Height" disabled><br><br>
            <h6> Calculated Field of View: </h6>
            <input type="text" id="calcfov" name="calcfov" value="Field of View" disabled><br><br>
            <button type="button"  id="execute" onclick="execute();"> Execute </button>
        </div>
        -->
    </div>

    <div class="row">
        <div class="col-12 text-center">
            <h6>Lens Focus Length:</h6>
            <input type="text" id="lensFocus" name="lensFocus" value="Focus Length" disabled><br> <br>
            <h6>Installation Height:</h6>
            <input type="text" id="instHeight" name="instHeight" value="Installation Height" disabled><br><br>
            <h6> Calculated Field of View: </h6>
            <input type="text" id="calcfov" name="calcfov" value="Field of View" disabled><br><br>
            <button type="button"  id="execute" onclick="execute();"> Execute </button> <br> <br> <br>
        </div>
    </div>

    <div class="row"> 
        <div class="col-12 text-center">
            <h5> <span id="title" class="text"> </span></h5>
        </div>
    </div>
<br> <br>

</form>
</body>
<script>
    var PreferredHeight
    var Angle
    var LensFocusLength
    var InstallationHeight
    var MaximumLength
    var CalculateFieldofView

    function calculate(){
        LensFocusLength=50
        Angle=32
        PreferredHeight= document.getElementById("preHeight").value
        MaximumLength= document.getElementById("maxLength").value
        
        // calculated installation
        InstallationHeight= 1/2 * (MaximumLength*1.1)/Math.tan(Angle/2 * Math.PI/180) + LensFocusLength + 112.6

   
        if ((PreferredHeight>=3000) && (PreferredHeight<InstallationHeight)) {
            LensFocusLength=40
            Angle=39
            InstallationHeight= 1/2 * (MaximumLength*1.1)/Math.tan(Angle/2 * Math.PI/180) + LensFocusLength + 112.6
        }     


        if ((PreferredHeight>=3000) && (InstallationHeight<PreferredHeight)) {
            InstallationHeight=PreferredHeight
        } 


       if ((InstallationHeight>4500) && (PreferredHeight<3000)) {
            LensFocusLength=40
            Angle=39
            InstallationHeight= 1/2 * (MaximumLength*1.1)/Math.tan(Angle/2 * Math.PI/180) + LensFocusLength + 112.6
        }

        InstallationHeight = Math.round(InstallationHeight)
        
        if (InstallationHeight<3000){
            InstallationHeight=3000
        }

 



        CalculateFieldofView= 2 * (InstallationHeight-LensFocusLength-112.6) * Math.tan (Angle/2 * Math.PI/180)
        CalculateFieldofView= Math.round(CalculateFieldofView)-1




        document.getElementById("lensFocus").value=LensFocusLength
        document.getElementById("calcfov").value= CalculateFieldofView
        document.getElementById("instHeight").value= InstallationHeight
  
    }
    function execute(){
        document.getElementById("title").style.color= "red"
        document.getElementById("title").innerHTML= "Thank you! Have a nice day :)"
    }
</script>


</html>
