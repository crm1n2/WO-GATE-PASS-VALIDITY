
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Industrial Live Dashboard</title>

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    background:#111827;
    color:white;
}

.header{
    padding:20px;
    background:#1f2937;
    text-align:center;
    font-size:28px;
    font-weight:bold;
}

.container{
    display:flex;
    flex-wrap:wrap;
    gap:20px;
    padding:20px;
    justify-content:center;
}

.card{
    background:#1e293b;
    border-radius:14px;
    padding:20px;
    width:280px;
    box-shadow:0 4px 10px rgba(0,0,0,0.3);
}

.title{
    font-size:20px;
    margin-bottom:10px;
}

.value{
    font-size:32px;
    font-weight:bold;
}

.updated{
    margin-top:10px;
    font-size:12px;
    color:#9ca3af;
}
</style>
</head>

<body>

<div class="header">
    Live Industrial Dashboard
</div>

<div class="container" id="dashboard"></div>

<script>

// ======= PASTE YOUR API BELOW =======
const API =
"https://docs.google.com/spreadsheets/d/1O7guxBa1XJOoBWwgzgBzRKhpG60iEgvjWMwcWIMyrYs/edit?gid=0#gid=0";
// ====================================

async function loadData(){

    try{

        const response = await fetch(API);
        const data = await response.json();

        const dashboard =
        document.getElementById("dashboard");

        dashboard.innerHTML = "";

        data.forEach(row => {

            dashboard.innerHTML += `
                <div class="card">
                    <div class="title">${row.Name || "Device"}</div>

                    <div class="value">
                        ${row.Value || "-"}
                    </div>

                    <p>Status: ${row.Status || "-"}</p>

                    <div class="updated">
                        Updated:
                        ${row.Updated || "-"}
                    </div>
                </div>
            `;
        });

    }
    catch(err){

        document.getElementById("dashboard")
        .innerHTML =
        "<h2>Error loading data</h2>";

        console.error(err);
    }
}

loadData();

setInterval(loadData,5000);

</script>

</body>
</html>
