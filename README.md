<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Accounting Client Dashboard</title>

    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

    <!-- Google APIs -->
    <script
        async
        defer
        src="https://apis.google.com/js/api.js"
        onload="gapiLoaded()">
    </script>

    <script
        async
        defer
        src="https://accounts.google.com/gsi/client"
        onload="gisLoaded()">
    </script>

    <style>

        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: #f4f6f9;
            color: #1f2937;
        }

        header {
            background: #1f2937;
            color: white;
            padding: 20px 30px;

            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .container {
            max-width: 1400px;
            margin: auto;
            padding: 30px;
        }

        .login {
            max-width: 420px;
            margin: 100px auto;
            background: white;
            padding: 35px;
            border-radius: 12px;
            box-shadow: 0 5px 25px rgba(0,0,0,.1);
        }

        input,
        select,
        textarea {
            width: 100%;
            padding: 11px;
            margin: 7px 0 15px;
            border: 1px solid #d1d5db;
            border-radius: 7px;
        }

        button {
            border: none;
            padding: 10px 16px;
            border-radius: 7px;
            cursor: pointer;
            background: #2563eb;
            color: white;
            margin-right: 5px;
        }

        button:hover {
            opacity: .9;
        }

        .logout {
            background: #dc2626;
        }

        .cards {
            display: grid;
            grid-template-columns:
                repeat(auto-fit, minmax(200px, 1fr));

            gap: 20px;
            margin-bottom: 30px;
        }

        .card {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 10px rgba(0,0,0,.06);
        }

        .card h2 {
            margin: 0;
            font-size: 30px;
        }

        .toolbar {
            background: white;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
        }

        table {
            width: 100%;
            background: white;
            border-collapse: collapse;
            border-radius: 10px;
            overflow: hidden;
        }

        th,
        td {
            padding: 13px;
            border-bottom: 1px solid #e5e7eb;
            text-align: left;
        }

        th {
            background: #374151;
            color: white;
        }

        .status {
            padding: 5px 9px;
            border-radius: 15px;
            font-size: 12px;
            font-weight: bold;
        }

        .under-review {
            background: #fef3c7;
        }

        .pending {
            background: #dbeafe;
        }

        .completed {
            background: #dcfce7;
        }

        .archived {
            background: #e5e7eb;
        }

        .overdue {
            background: #fee2e2;
            color: #991b1b;
        }

        .modal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,.5);
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            width: 90%;
            max-width: 700px;
            background: white;
            padding: 30px;
            border-radius: 12px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .drive-button {
            background: #16a34a;
        }

        .hidden {
            display: none !important;
        }

        @media(max-width: 800px) {

            table {
                font-size: 12px;
            }

            .container {
                padding: 15px;
            }

        }

    </style>
</head>


<body>

<!-- LOGIN -->

<div id="loginPage" class="login">

    <h1>Accounting Dashboard</h1>

    <p>Sign in to continue.</p>

    <input
        type="email"
        id="email"
        placeholder="Email">

    <input
        type="password"
        id="password"
        placeholder="Password">

    <button onclick="login()">
        Login
    </button>

    <p id="loginMessage"></p>

</div>


<!-- APPLICATION -->

<div id="app" class="hidden">

    <header>

        <div>
            <h2>Client Accounting Dashboard</h2>
            <span id="userRole"></span>
        </div>

        <button
            class="logout"
            onclick="logout()">
            Logout
        </button>

    </header>


    <div class="container">


        <!-- DASHBOARD CARDS -->

        <div class="cards">

            <div class="card">
                <h4>Total Clients</h4>
                <h2 id="totalClients">0</h2>
            </div>

            <div class="card">
                <h4>Under Review</h4>
                <h2 id="reviewClients">0</h2>
            </div>

            <div class="card">
                <h4>Pending</h4>
                <h2 id="pendingClients">0</h2>
            </div>

            <div class="card">
                <h4>Completed</h4>
                <h2 id="completedClients">0</h2>
            </div>

            <div class="card">
                <h4>Overdue</h4>
                <h2 id="overdueClients">0</h2>
            </div>

            <div class="card">
                <h4>Outstanding</h4>
                <h2 id="outstanding">$0</h2>
            </div>

        </div>


        <!-- TOOLBAR -->

        <div class="toolbar">

            <button onclick="openNewClient()">
                + Add Client
            </button>

            <input
                id="search"
                placeholder="Search clients..."
                oninput="renderClients()">

            <select
                id="statusFilter"
                onchange="renderClients()">

                <option value="">All Statuses</option>
                <option>Under Review</option>
                <option>Pending</option>
                <option>Completed</option>
                <option>Archived</option>
                <option>Overdue</option>

            </select>

        </div>


        <!-- CLIENT TABLE -->

        <table>

            <thead>

                <tr>

                    <th>Client</th>
                    <th>Contact</th>
                    <th>Service</th>
                    <th>Invoice</th>
                    <th>Amount</th>
                    <th>Due</th>
                    <th>Status</th>
                    <th>Drive</th>
                    <th>Actions</th>

                </tr>

            </thead>

            <tbody id="clientTable"></tbody>

        </table>


    </div>

</div>


<!-- CLIENT MODAL -->

<div
    id="clientModal"
    class="modal">

    <div class="modal-content">

        <h2 id="modalTitle">
            Add Client
        </h2>

        <input
            type="hidden"
            id="clientId">

        <label>Company Name</label>
        <input id="companyName">

        <label>Contact Name</label>
        <input id="contactName">

        <label>Email</label>
        <input id="clientEmail">

        <label>Phone</label>
        <input id="clientPhone">

        <label>Service</label>
        <input id="service">

        <label>Invoice Number</label>
        <input id="invoiceNumber">

        <label>Invoice Amount</label>
        <input
            type="number"
            id="invoiceAmount"
            step="0.01">

        <label>Due Date</label>
        <input
            type="date"
            id="dueDate">

        <label>Status</label>

        <select id="clientStatus">

            <option>Under Review</option>
            <option>Pending</option>
            <option>Completed</option>
            <option>Archived</option>
            <option>Overdue</option>

        </select>


        <label>Notes</label>

        <textarea
            id="notes"
            rows="5"></textarea>


        <label>Google Drive</label>

        <input
            id="driveFolderUrl"
            placeholder="Selected Drive file/folder URL">

        <button
            class="drive-button"
            onclick="openDrivePicker()">

            Connect Google Drive

        </button>


        <br><br>

        <button onclick="saveClient()">
            Save Client
        </button>

        <button
            onclick="closeModal()">
            Cancel
        </button>

    </div>

</div>


<script>

/* ========================================
   SUPABASE
======================================== */

const SUPABASE_URL =
    "YOUR_SUPABASE_URL";

const SUPABASE_ANON_KEY =
    "YOUR_SUPABASE_ANON_KEY";


const supabaseClient =
    supabase.createClient(
        SUPABASE_URL,
        SUPABASE_ANON_KEY
    );


let clients = [];
let currentRole = null;


/* ========================================
   GOOGLE CONFIG
======================================== */

const GOOGLE_CLIENT_ID =
    "YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com";

const GOOGLE_API_KEY =
    "YOUR_GOOGLE_API_KEY";

const GOOGLE_APP_ID =
    "YOUR_GOOGLE_CLOUD_PROJECT_NUMBER";


let tokenClient;
let accessToken = null;

let pickerReady = false;
let gisReady = false;


/* ========================================
   LOGIN
======================================== */

async function login() {

    const email =
        document.getElementById("email").value;

    const password =
        document.getElementById("password").value;


    const { error } =
        await supabaseClient.auth.signInWithPassword({
            email,
            password
        });


    if (error) {

        document.getElementById(
            "loginMessage"
        ).innerText = error.message;

        return;
    }

    await initializeApp();

}


/* ========================================
   INITIALIZE
======================================== */

async function initializeApp() {

    const {
        data: { user }
    } = await supabaseClient.auth.getUser();


    if (!user) return;


    const { data: role } =
        await supabaseClient
        .from("user_roles")
        .select("role")
        .eq("user_id", user.id)
        .single();


    if (!role) {

        alert(
            "Your account has not been assigned a role."
        );

        return;
    }


    currentRole = role.role;


    document.getElementById(
        "loginPage"
    ).classList.add("hidden");


    document.getElementById(
        "app"
    ).classList.remove("hidden");


    document.getElementById(
        "userRole"
    ).innerText =
        "Logged in as: " + currentRole;


    await loadClients();

}


/* ========================================
   LOAD CLIENTS
======================================== */

async function loadClients() {

    const { data, error } =
        await supabaseClient
        .from("clients")
        .select("*")
        .order("created_at", {
            ascending: false
        });


    if (error) {

        alert(error.message);

        return;
    }


    clients = data || [];

    updateDashboard();

    renderClients();

}


/* ========================================
   DASHBOARD
======================================== */

function updateDashboard() {

    document.getElementById(
        "totalClients"
    ).innerText = clients.length;


    document.getElementById(
        "reviewClients"
    ).innerText =
        clients.filter(
            x => x.status === "Under Review"
        ).length;


    document.getElementById(
        "pendingClients"
    ).innerText =
        clients.filter(
            x => x.status === "Pending"
        ).length;


    document.getElementById(
        "completedClients"
    ).innerText =
        clients.filter(
            x => x.status === "Completed"
        ).length;


    document.getElementById(
        "overdueClients"
    ).innerText =
        clients.filter(
            x => x.status === "Overdue"
        ).length;


    const outstanding =
        clients
        .filter(x => x.status !== "Completed")
        .reduce(
            (sum, x) =>
                sum + Number(x.invoice_amount || 0),
            0
        );


    document.getElementById(
        "outstanding"
    ).innerText =
        "$" + outstanding.toLocaleString(
            undefined,
            {
                minimumFractionDigits: 2
            }
        );

}


/* ========================================
   CLIENT TABLE
======================================== */

function renderClients() {

    const search =
        document.getElementById(
            "search"
        ).value.toLowerCase();


    const status =
        document.getElementById(
            "statusFilter"
        ).value;


    const filtered =
        clients.filter(client => {

            const text =
                `${client.company_name}
                ${client.contact_name}
                ${client.service}
                ${client.invoice_number}`
                .toLowerCase();


            return (
                text.includes(search) &&
                (!status || client.status === status)
            );

        });


    const table =
        document.getElementById(
            "clientTable"
        );


    table.innerHTML = "";


    filtered.forEach(client => {

        const row =
            document.createElement("tr");


        const statusClass =
            client.status
            .toLowerCase()
            .replaceAll(" ", "-");


        row.innerHTML = `

            <td>
                <strong>
                    ${escapeHtml(client.company_name)}
                </strong>
            </td>

            <td>
                ${escapeHtml(client.contact_name || "")}
                <br>
                ${escapeHtml(client.email || "")}
            </td>

            <td>
                ${escapeHtml(client.service || "")}
            </td>

            <td>
                ${escapeHtml(client.invoice_number || "")}
            </td>

            <td>
                $${Number(
                    client.invoice_amount || 0
                ).toFixed(2)}
            </td>

            <td>
                ${client.due_date || ""}
            </td>

            <td>
                <span class="status ${statusClass}">
                    ${client.status}
                </span>
            </td>

            <td>

                ${
                    client.drive_folder_url
                    ?
                    `<a
                        href="${escapeAttribute(client.drive_folder_url)}"
                        target="_blank">
                        Open Drive
                    </a>`
                    :
                    "Not connected"
                }

            </td>

            <td>

                <button
                    onclick="editClient('${client.id}')">
                    Edit
                </button>

                ${
                    currentRole === "admin"
                    ?
                    `
                    <button
                        onclick="deleteClient('${client.id}')">
                        Delete
                    </button>
                    `
                    :
                    ""
                }

            </td>

        `;


        table.appendChild(row);

    });

}


/* ========================================
   NEW CLIENT
======================================== */

function openNewClient() {

    document.getElementById(
        "modalTitle"
    ).innerText = "Add Client";


    document.getElementById(
        "clientId"
    ).value = "";


    clearForm();


    document.getElementById(
        "clientModal"
    ).style.display = "flex";

}


function clearForm() {

    [
        "companyName",
        "contactName",
        "clientEmail",
        "clientPhone",
        "service",
        "invoiceNumber",
        "invoiceAmount",
        "dueDate",
        "notes",
        "driveFolderUrl"

    ].forEach(id => {

        document.getElementById(id).value = "";

    });


    document.getElementById(
        "clientStatus"
    ).value = "Under Review";

}


/* ========================================
   EDIT CLIENT
======================================== */

function editClient(id) {

    const client =
        clients.find(x => x.id === id);


    if (!client) return;


    document.getElementById(
        "modalTitle"
    ).innerText = "Edit Client";


    document.getElementById(
        "clientId"
    ).value = client.id;


    document.getElementById(
        "companyName"
    ).value =
        client.company_name || "";


    document.getElementById(
        "contactName"
    ).value =
        client.contact_name || "";


    document.getElementById(
        "clientEmail"
    ).value =
        client.email || "";


    document.getElementById(
        "clientPhone"
    ).value =
        client.phone || "";


    document.getElementById(
        "service"
    ).value =
        client.service || "";


    document.getElementById(
        "invoiceNumber"
    ).value =
        client.invoice_number || "";


    document.getElementById(
        "invoiceAmount"
    ).value =
        client.invoice_amount || 0;


    document.getElementById(
        "dueDate"
    ).value =
        client.due_date || "";


    document.getElementById(
        "clientStatus"
    ).value =
        client.status;


    document.getElementById(
        "notes"
    ).value =
        client.notes || "";


    document.getElementById(
        "driveFolderUrl"
    ).value =
        client.drive_folder_url || "";


    document.getElementById(
        "clientModal"
    ).style.display = "flex";

}


/* ========================================
   SAVE CLIENT
======================================== */

async function saveClient() {

    const {
        data: { user }
    } =
        await supabaseClient.auth.getUser();


    const id =
        document.getElementById(
            "clientId"
        ).value;


    const record = {

        company_name:
            document.getElementById(
                "companyName"
            ).value,

        contact_name:
            document.getElementById(
                "contactName"
            ).value,

        email:
            document.getElementById(
                "clientEmail"
            ).value,

        phone:
            document.getElementById(
                "clientPhone"
            ).value,

        service:
            document.getElementById(
                "service"
            ).value,

        invoice_number:
            document.getElementById(
                "invoiceNumber"
            ).value,

        invoice_amount:
            Number(
                document.getElementById(
                    "invoiceAmount"
                ).value || 0
            ),

        due_date:
            document.getElementById(
                "dueDate"
            ).value || null,

        status:
            document.getElementById(
                "clientStatus"
            ).value,

        notes:
            document.getElementById(
                "notes"
            ).value,

        drive_folder_url:
            document.getElementById(
                "driveFolderUrl"
            ).value,

        updated_by: user.id

    };


    let result;


    if (id) {

        result =
            await supabaseClient
            .from("clients")
            .update(record)
            .eq("id", id);

    } else {

        record.created_by =
            user.id;

        result =
            await supabaseClient
            .from("clients")
            .insert(record);

    }


    if (result.error) {

        alert(result.error.message);

        return;
    }


    closeModal();

    await loadClients();

}


/* ========================================
   DELETE CLIENT
======================================== */

async function deleteClient(id) {

    if (
        currentRole !== "admin"
    ) return;


    if (
        !confirm(
            "Delete this client?"
        )
    ) return;


    const { error } =
        await supabaseClient
        .from("clients")
        .delete()
        .eq("id", id);


    if (error) {

        alert(error.message);

        return;
    }


    await loadClients();

}


/* ========================================
   CLOSE MODAL
======================================== */

function closeModal() {

    document.getElementById(
        "clientModal"
    ).style.display = "none";

}


/* ========================================
   GOOGLE PICKER
======================================== */

function gapiLoaded() {

    gapi.load(
        "picker",
        () => {
            pickerReady = true;
        }
    );

}


function gisLoaded() {

    tokenClient =
        google.accounts.oauth2.initTokenClient({

            client_id:
                GOOGLE_CLIENT_ID,

            scope:
                "https://www.googleapis.com/auth/drive.readonly",

            callback: ""

        });


    gisReady = true;

}


function openDrivePicker() {

    if (
        !pickerReady ||
        !gisReady
    ) {

        alert(
            "Google Drive is still loading. Try again in a moment."
        );

        return;
    }


    tokenClient.callback =
        response => {

            if (response.error) {

                console.error(response);

                return;
            }


            accessToken =
                response.access_token;


            const view =
                new google.picker.DocsView(
                    google.picker.ViewId.DOCS
                );


            const picker =
                new google.picker.PickerBuilder()

                .setDeveloperKey(
                    GOOGLE_API_KEY
                )

                .setAppId(
                    GOOGLE_APP_ID
                )

                .setOAuthToken(
                    accessToken
                )

                .addView(view)

                .setCallback(
                    pickerCallback
                )

                .build();


            picker.setVisible(true);

        };


    tokenClient.requestAccessToken({
        prompt: ""
    });

}


function pickerCallback(data) {

    if (
        data.action ===
        google.picker.Action.PICKED
    ) {

        const file =
            data.docs[0];


        document.getElementById(
            "driveFolderUrl"
        ).value =
            file.url;

    }

}


/* ========================================
   LOGOUT
======================================== */

async function logout() {

    await supabaseClient.auth.signOut();

    location.reload();

}


/* ========================================
   XSS PROTECTION
======================================== */

function escapeHtml(value) {

    return String(value)
        .replaceAll("&", "&amp;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;")
        .replaceAll('"', "&quot;")
        .replaceAll("'", "&#039;");

}


function escapeAttribute(value) {

    return String(value)
        .replaceAll('"', "&quot;");

}


/* ========================================
   AUTO LOGIN
======================================== */

supabaseClient.auth.onAuthStateChange(
    async (event, session) => {

        if (session) {

            await initializeApp();

        }

    }
);

</script>

</body>
</html>
