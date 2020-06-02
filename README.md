<html lang="en">
<head>
    <title>HMD2048 Calculation</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- Latest compiled and minified CSS -->
    <link rel="stylesheet"
          href="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
    <!-- jQuery library -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
    <!-- Popper JS -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
    <!-- Latest compiled JavaScript -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>

    <body>

        <div class="row">
            <BR><BR>
        </div>
        <div class="row">
            <div class="col-12 text-center">
                <h6> Maximum Roll Length (mm) </h6>
                <input type="text" id="maxLength" name="maxLength" value=""><br> <br>
                <h6>Preferred Installation Height (mm)</h6>
                <input type="text" id="preHeight" name="preHeight" value=""><br><br>
                <button type="button" id="calculate" onclick="calculate();">Calculate</button> <br> <BR> <BR>
            </div>

        </div>

        <div class="row">
            <div class="col-12 text-center">
                <h6>Lens Focus Length (mm)</h6>
                <input type="text" id="lensFocus" name="lensFocus" value="Focus Length" disabled><br> <br>
                <h6>Installation Height (mm)</h6>
                <input type="text" id="instHeight" name="instHeight" value="Installation Height" disabled><br><br>
                <h6> Calculated Field of View (mm)</h6>
                <input type="text" id="calcfov" name="calcfov" value="Field of View" disabled><br><br>
                <button type="button" id="execute" onclick="download_csv();"> Create WorkOrder </button> <br> <br> <br>
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
        var HMD2048Table = [
            ['1', 'M', '1', 'EA', 'HMD2048-TBA', 'ACCUSCAN SYSTEM', ' ', 'MFG', ' ', ' ', ' ', ' ', ' '],
            ['2', 'M1', '1', 'EA', 'PL054588', ' ', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['3', 'M2', '1', 'EA', ' ', ' ', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['4', 'M3', '1', 'EA', 'PL054836', 'Nozzle Assembly', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['5', 'M4', '1', 'EA', 'PL054854', 'Mounting Bracket   ', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['6', 'M5', '1', 'EA', 'PL057355', 'Junction Box WITH Serial Server', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['7', 'M6', '1', 'EA', 'PL053322-15M', 'HMD2048 Cable Assembly 15m', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['8', 'M7', '1', 'EA', 'PL054926', 'HMD2048 Accessory Kit', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['9', 'M8', '1', 'EA', '054908-1', ' UAP HMD2048 Rev.C & User Manual on CD ', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['10', 'M9', '1', 'EA', 'PL055980', ' HMD2048 Heat insulation and Reflector', ' ', 'STK', ' ', ' ', ' ', ' ', '1'],
            ['11', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '],
            ['12', 'H', ' ', ' ', ' ', 'ENGINEERING SERVICES', ' ', ' ', ' ', ' ', ' ', ' ', ' '],
            ['13', 'H1', '1', 'EA', ' ', ' Project Engineering', ' ', 'ENG ', ' ', ' ', ' ', ' ', ' '],
            ['14', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '],
            ['15', 'J', ' ', ' ', ' ', 'COMMISSIONING AND TRAINING ', ' ', ' ', ' ', ' ', ' ', ' ', ' '],
            ['16', 'J1', '1', 'EA', ' ', ' see  Field Service TBA', ' ', 'ENG ', ' ', ' ', ' ', ' ', ' '],
            ['17', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '],
            ['18', 'K', ' ', ' ', ' ', 'DOCUMENTATION', ' ', ' ', ' ', ' ', ' ', ' ', ' '],
            ['19', 'K1', '1', 'EA', '90386', ' Accuscan HMD2048 User Manual   ', ' ', 'ENG ', ' ', ' ', ' ', ' ', ' '],
            ['20', 'K2', '1', 'EA', '58960', ' Accuscan HMD2048 System Drawing Package', ' ', 'REF ', ' ', ' ', ' ', ' ', ' '],
            ['21', 'K3', '1', 'EA', '054908-1', ' UAP HMD2048 Rev. C & User Manual on CD ', ' ', 'REF', ' ', ' ', ' ', ' ', ''],
            ['22', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '],
            ['23', 'T', ' ', ' ', ' ', 'ADDITIONAL PRODUCTION TESTING', ' ', ' ', ' ', ' ', ' ', ' ', ' ']

        ];

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

        InstallationHeight=Math.round(InstallationHeight/10 ) * 10

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

        HMD2048Table[1][5] = "HMD2048 Camera Assembly (Installation Height:" + InstallationHeight + 'mm)'

        if (LensFocusLength == 40) {
            HMD2048Table[2][4] = "PL056193-IR"
            HMD2048Table[2][5] = "Optics Kit Assembly 40mm IR"
        } else {
            HMD2048Table[2][4] = "PL056194-IR"
            HMD2048Table[2][5] = "Optics Kit Assembly 50mm IR"
        }
    }

        function download_csv() {
            var csv = 'HMD2048,Item,QTY,UOM,PartNumber,Description,SN,Status,FolderDate,MFGDate,ShipDate,Tran,Crate\n';
            HMD2048Table.forEach(function (row) {
                csv += row.join(',');
                csv += "\n";
            });

            console.log(csv);
            var hiddenElement = document.createElement('a');
            hiddenElement.href = 'data:text/csv;charset=utf-8,' + encodeURI(csv);
            hiddenElement.target = '_blank';
            hiddenElement.download = 'HMD2048.csv';
            hiddenElement.click();
        }



    function execute(){
        document.getElementById("title").style.color= "red"
        document.getElementById("title").innerHTML= "Thank you! Have a nice day :)"
    }</script>


</html>
