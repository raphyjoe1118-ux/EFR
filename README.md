<Accounting Solutions>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>EFR Accounting Firm | Client Dashboard</title>

    <!-- Supabase -->
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

    <!-- Google Picker -->
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
            font-family: Arial, Helvetica, sans-serif;
            background: #f4f6f8;
            color: #1f2937;
        }

        /* =========================
           LOGIN
        ========================= */

        #loginPage {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .login-box {
            width: 100%;
            max-width: 430px;
            background: white;
            padding: 40px;
            border-radius: 16px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.10);
        }

        .login-logo {
            text-align: center;
            margin-bottom: 30px;
        }

        .login-logo .logo-circle {
            width: 65px;
            height: 65px;
            border-radius: 50%;
            margin: 0 auto 15px;
            background: #163a5f;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            font-weight: bold;
        }

        .login-logo h1 {
            margin: 0;
            color: #163a5f;
        }

        .login-logo p {
            color: #6b7280;
            margin-top: 8px;
        }

        /* =========================
           APPLICATION
        ========================= */

        .hidden {
            display: none !important;
        }

        .topbar {
            background: #163a5f;
            color: white;
            padding: 18px 30px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,.12);
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 14px;
        }

        .brand-logo {
            width: 46px;
            height: 46px;
            background: white;
            color: #163a5f;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .brand h2 {
            margin: 0;
            font-size: 21px;
        }

        .brand small {
            display: block;
            margin-top: 3px;
            opacity: .85;
        }

        .topbar-right {
            display: flex;
            align-items: center;
            gap: 14px;
        }

        .user-role {
            font-size: 14px;
            opacity: .9;
        }

        .container {
            max-width: 1500px;
            margin: 0 auto;
            padding: 30px;
        }

        /* =========================
           BUTTONS
        ========================= */

        button {
            border: none;
            border-radius: 7px;
            padding: 10px 15px;
            cursor: pointer;
            font-size: 14px;
            transition: .2s;
        }

        button:hover {
            opacity: .9;
        }

        .btn-primary {
            background: #2563eb;
            color: white;
        }

        .btn-danger {
            background: #dc2626;
            color: white;
        }

        .btn-success {
            background: #16a34a;
            color: white;
        }

        .btn-secondary {
            background: #6b7280;
            color: white;
        }

        .btn-light {
            background: #e5e7eb;
            color: #1f2937;
        }

        /* =========================
           DASHBOARD CARDS
        ========================= */

        .cards {
            display: grid;
            grid-template-columns: repeat(
                auto-fit,
                minmax(190px, 1fr)
            );
            gap: 18px;
            margin-bottom: 25px;
        }

        .card {
            background: white;
            border-radius: 12px;
            padding: 22px;
            box-shadow: 0 2px 10px rgba(0,0,0,.05);
        }

        .card h4 {
            margin: 0 0 10px;
            color: #6b7280;
            font-size: 14px;
            font-weight: normal;
        }

        .card h2 {
            margin: 0;
            font-size: 28px;
            color: #163a5f;
        }

        /* =========================
           TOOLBAR
        ========================= */

        .toolbar {
            background: white;
            padding: 18px;
            border-radius: 12px;
            margin-bottom: 20px;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }

        .toolbar input,
        .toolbar select {
            width: auto;
            min-width: 220px;
            margin: 0;
        }

        /* =========================
           TABLE
        ========================= */

        .table-container {
            background: white;
            border-radius: 12px;
            overflow-x: auto;
            box-shadow: 0 2px 10px rgba(0,0,0,.05);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 1100px;
        }

        th,
        td {
            padding: 13px 14px;
            text-align: left;
            border-bottom: 1px solid #e5e7eb;
        }

        th {
            background: #1f2937;
            color: white;
            font-size: 13px;
        }

        td {
            font-size: 14px;
        }

        tr:hover td {
            background: #f9fafb;
        }

        /* =========================
           STATUS
        ========================= */

        .status {
            display: inline-block;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
            white-space: nowrap;
        }

        .status-under-review {
            background: #fef3c7;
            color: #92400e;
        }

        .status-pending {
            background: #dbeafe;
            color: #1e40af;
        }

        .status-completed {
            background: #dcfce7;
            color: #166534;
        }

        .status-archived {
            background: #e5e7eb;
            color: #374151;
        }

        .status-overdue {
            background: #fee2e2;
            color: #991b1b;
        }

        /* =========================
           FORMS
        ========================= */

        input,
        select,
        textarea {
            width: 100%;
            padding: 11px 12px;
            border: 1px solid #d1d5db;
            border-radius: 7px;
            font: inherit;
            background: white;
        }

        label {
            display: block;
            font-weight: 600;
            margin-bottom: 6px;
            font-size: 14px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }

        .form-grid .full {
            grid-column: 1 / -1;
        }

        /* =========================
           MODAL
        ========================= */

        .modal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,.50);
            justify-content: center;
            align-items: center;
            padding: 20px;
            z-index: 1000;
        }

        .modal-content {
            background: white;
            width: 100%;
            max-width: 800px;
            max-height: 92vh;
            overflow-y: auto;
            padding: 30px;
            border-radius: 14px;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .modal-header h2 {
            margin: 0;
            color: #163a5f;
        }

        .modal-footer {
            margin-top: 20px;
            display: flex;
            gap: 8px;
        }

        .drive-row {
            display: flex;
            gap: 8px;
        }

        .drive-row input {
            flex: 1;
        }

        /* =========================
           MESSAGES
        ========================= */

        .message {
            margin-top: 15px;
            font-size: 14px;
        }

        .error {
            color: #dc2626;
        }

        .success {
            color: #16a34a;
        }

        .empty-state {
            text-align: center;
            padding: 50px;
            color: #6b7280;
        }

        a {
            color: #2563eb;
            text-decoration: none;
        }

        a:hover {
            text-decoration: underline;
        }

        /* =========================
           MOBILE
        ========================= */

        @media (max-width: 700px) {

            .topbar {
                flex-direction: column;
                align-items: flex-start;
            }

            .topbar-right {
                width: 100%;
                justify-content: space-between;
            }

            .container {
                padding: 15px;
            }

            .form-grid {
                grid-template-columns: 1fr;
            }

            .form-grid .full {
                grid-column: auto;
            }

            .toolbar input,
            .toolbar select {
                width: 100%;
            }

        }
    </style>
</head>

<body>

<!-- =========================================================
     LOGIN PAGE
========================================================= -->

<div id="loginPage">

    <div class="login-box">

        <div class="login-logo">

            <div class="logo-circle">
                EFR
            </div>

            <h1>EFR Accounting Firm</h1>

            <p>Client Management Portal</p>

        </div>

        <div class="form-group">

            <label for="email">
                Email
            </label>

            <input
                type="email"
                id="email"
                placeholder="Enter your email"
                autocomplete="email">

        </div>

        <div class="form-group">

            <label for="password">
                Password
            </label>

            <input
                type="password"
                id="password"
                placeholder="Enter your password"
                autocomplete="current-password">

        </div>

        <button
            class="btn-primary"
            style="width:100%;"
            onclick="login()">

            Login

        </button>

        <div
            id="loginMessage"
            class="message">
        </div>

    </div>

</div>


<!-- =========================================================
     MAIN APPLICATION
========================================================= -->

<div id="app" class="hidden">

    <header class="topbar">

        <div class="brand">

            <div class="brand-logo">
                EFR
            </div>

            <div>

                <h2>EFR Accounting Firm</h2>

                <small>
                    Client Accounting Dashboard
                </small>

            </div>

        </div>

        <div class="topbar-right">

            <span
                class="user-role"
                id="userRole">
            </span>

            <button
                class="btn-danger"
                onclick="logout()">

                Logout

            </button>

        </div>

    </header>


    <main class="container">

        <!-- DASHBOARD -->

        <section class="cards">

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
                <h2 id="outstanding">$0.00</h2>
            </div>

        </section>


        <!-- TOOLBAR -->

        <section class="toolbar">

            <button
                class="btn-primary"
                onclick="openNewClient()">

                + Add Client

            </button>

            <input
                type="search"
                id="search"
                placeholder="Search clients..."
                oninput="renderClients()">

            <select
                id="statusFilter"
                onchange="renderClients()">

                <option value="">
                    All Statuses
                </option>

                <option>
                    Under Review
                </option>

                <option>
                    Pending
                </option>

                <option>
                    Completed
                </option>

                <option>
                    Archived
                </option>

                <option>
                    Overdue
                </option>

            </select>

        </section>


        <!-- CLIENT TABLE -->

        <section class="table-container">

            <table>

                <thead>

                    <tr>

                        <th>Client</th>
                        <th>Contact</th>
                        <th>Service</th>
                        <th>Invoice</th>
                        <th>Amount</th>
                        <th>Due Date</th>
                        <th>Status</th>
                        <th>Google Drive</th>
                        <th>Actions</th>

                    </tr>

                </thead>

                <tbody id="clientTable"></tbody>

            </table>

        </section>

    </main>

</div>


<!-- =========================================================
     CLIENT MODAL
========================================================= -->

<div
    id="clientModal"
    class="modal">

    <div class="modal-content">

        <div class="modal-header">

            <h2 id="modalTitle">
                Add Client
            </h2>

            <button
                class="btn-light"
                onclick="closeModal()">

                ✕

            </button>

        </div>


        <input
            type="hidden"
            id="clientId">


        <div class="form-grid">

            <div class="form-group">

                <label>
                    Company Name *
                </label>

                <input
                    id="companyName"
                    placeholder="ABC Company">

            </div>


            <div class="form-group">

                <label>
                    Contact Name
                </label>

                <input
                    id="contactName"
                    placeholder="John Smith">

            </div>


            <div class="form-group">

                <label>
                    Email
                </label>

                <input
                    type="email"
                    id="clientEmail"
                    placeholder="client@example.com">

            </div>


            <div class="form-group">

                <label>
                    Phone
                </label>

                <input
                    id="clientPhone"
                    placeholder="555-555-5555">

            </div>


            <div class="form-group">

                <label>
                    Service
                </label>

                <input
                    id="service"
                    placeholder="Bookkeeping">

            </div>


            <div class="form-group">

                <label>
                    Invoice Number
                </label>

                <input
                    id="invoiceNumber"
                    placeholder="INV-1001">

            </div>


            <div class="form-group">

                <label>
                    Invoice Amount
                </label>

                <input
                    type="number"
                    id="invoiceAmount"
                    step="0.01"
                    min="0"
                    placeholder="0.00">

            </div>


            <div class="form-group">

                <label>
                    Due Date
                </label>

                <input
                    type="date"
                    id="dueDate">

            </div>


            <div class="form-group">

                <label>
                    Status
                </label>

                <select id="clientStatus">

                    <option>
                        Under Review
                    </option>

                    <option>
                        Pending
                    </option>

                    <option>
                        Completed
                    </option>

                    <option>
                        Archived
                    </option>

                    <option>
                        Overdue
                    </option>

                </select>

            </div>


            <div class="form-group full">

                <label>
                    Notes
                </label>

                <textarea
                    id="notes"
                    rows="5"
                    placeholder="Client notes...">
                </textarea>

            </div>


            <div class="form-group full">

                <label>
                    Google Drive
                </label>

                <div class="drive-row">

                    <input
                        id="driveFolderUrl"
                        placeholder="Drive file or folder URL">

                    <button
                        type="button"
                        class="btn-success"
                        onclick="openDrivePicker()">

                        Select from Drive

                    </button>

                </div>

            </div>

        </div>


        <div class="modal-footer">

            <button
                class="btn-primary"
                onclick="saveClient()">

                Save Client

            </button>

            <button
                class="btn-secondary"
                onclick="closeModal()">

                Cancel

            </button>

        </div>

    </div>

</div>


<script>

/* =========================================================
   CONFIGURATION
   REPLACE THESE VALUES
========================================================= */

const SUPABASE_URL =
    "YOUR_SUPABASE_URL";

const SUPABASE_ANON_KEY =
    "YOUR_SUPABASE_ANON_KEY";


const GOOGLE_CLIENT_ID =
    "YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com";

const GOOGLE_API_KEY =
    "YOUR_GOOGLE_API_KEY";

const GOOGLE_APP_ID =
    "YOUR_GOOGLE_PROJECT_NUMBER";


/* =========================================================
   GLOBAL VARIABLES
========================================================= */

const supabaseClient =
    supabase.createClient(
        SUPABASE_URL,
        SUPABASE_ANON_KEY
    );

let clients = [];

let currentRole = null;

let currentUser = null;

let tokenClient = null;

let accessToken = null;

let pickerReady = false;

let gisReady = false;


/* =========================================================
   LOGIN
========================================================= */

async function login() {

    const email =
        document.getElementById("email").value.trim();

    const password =
        document.getElementById("password").value;


    const message =
        document.getElementById("loginMessage");


    message.textContent = "";

    message.className = "message";


    if (!email || !password) {

        message.textContent =
            "Please enter your email and password.";

        message.classList.add("error");

        return;

    }


    const { data, error } =
        await supabaseClient.auth.signInWithPassword({
            email,
            password
        });


    if (error) {

        message.textContent =
            error.message;

        message.classList.add("error");

        return;

    }


    currentUser = data.user;

    await initializeApp();

}


/* =========================================================
   INITIALIZE APPLICATION
========================================================= */

async function initializeApp() {

    const {
        data: { user }
    } =
        await supabaseClient.auth.getUser();


    if (!user) {

        return;

    }


    currentUser = user;


    const { data: roleData, error } =
        await supabaseClient
        .from("user_roles")
        .select("role")
        .eq("user_id", user.id)
        .single();


    if (error || !roleData) {

        alert(
            "Your account does not have an assigned role. Contact the EFR Accounting Firm administrator."
        );

        await supabaseClient.auth.signOut();

        return;

    }


    currentRole = roleData.role;


    document
        .getElementById("loginPage")
        .classList.add("hidden");


    document
        .getElementById("app")
        .classList.remove("hidden");


    document
        .getElementById("userRole")
        .textContent =
            "Signed in as " +
            currentRole.toUpperCase();


    await loadClients();

}


/* =========================================================
   LOAD CLIENTS
========================================================= */

async function loadClients() {

    const { data, error } =
        await supabaseClient
        .from("clients")
        .select("*")
        .order("created_at", {
            ascending: false
        });


    if (error) {

        alert(
            "Unable to load clients: " +
            error.message
        );

        return;

    }


    clients = data || [];

    updateDashboard();

    renderClients();

}


/* =========================================================
   DASHBOARD METRICS
========================================================= */

function updateDashboard() {

    document.getElementById(
        "totalClients"
    ).textContent =
        clients.length;


    document.getElementById(
        "reviewClients"
    ).textContent =
        clients.filter(
            client =>
                client.status === "Under Review"
        ).length;


    document.getElementById(
        "pendingClients"
    ).textContent =
        clients.filter(
            client =>
                client.status === "Pending"
        ).length;


    document.getElementById(
        "completedClients"
    ).textContent =
        clients.filter(
            client =>
                client.status === "Completed"
        ).length;


    document.getElementById(
        "overdueClients"
    ).textContent =
        clients.filter(
            client =>
                client.status === "Overdue"
        ).length;


    const outstanding =
        clients
            .filter(
                client =>
                    client.status !== "Completed"
            )
            .reduce(
                (total, client) =>
                    total +
                    Number(
                        client.invoice_amount || 0
                    ),
                0
            );


    document.getElementById(
        "outstanding"
    ).textContent =
        "$" +
        outstanding.toLocaleString(
            "en-US",
            {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            }
        );

}


/* =========================================================
   CLIENT TABLE
========================================================= */

function renderClients() {

    const search =
        document
            .getElementById("search")
            .value
            .toLowerCase()
            .trim();


    const selectedStatus =
        document.getElementById(
            "statusFilter"
        ).value;


    const filtered =
        clients.filter(client => {

            const searchableText =
                [
                    client.company_name,
                    client.contact_name,
                    client.email,
                    client.phone,
                    client.service,
                    client.invoice_number,
                    client.notes
                ]
                .filter(Boolean)
                .join(" ")
                .toLowerCase();


            const matchesSearch =
                searchableText.includes(search);


            const matchesStatus =
                !selectedStatus ||
                client.status === selectedStatus;


            return (
                matchesSearch &&
                matchesStatus
            );

        });


    const table =
        document.getElementById(
            "clientTable"
        );


    table.innerHTML = "";


    if (filtered.length === 0) {

        table.innerHTML = `
            <tr>
                <td
                    colspan="9"
                    class="empty-state">

                    No clients found.

                </td>
            </tr>
        `;

        return;

    }


    filtered.forEach(client => {

        const row =
            document.createElement("tr");


        const statusClass =
            getStatusClass(
                client.status
            );


        row.innerHTML = `

            <td>

                <strong>
                    ${escapeHtml(
                        client.company_name || ""
                    )}
                </strong>

                ${
                    client.notes
                        ?
                        `<br>
                         <small>
                            ${escapeHtml(
                                client.notes
                            )}
                         </small>`
                        :
                        ""
                }

            </td>


            <td>

                ${escapeHtml(
                    client.contact_name || ""
                )}

                ${
                    client.email
                        ?
                        `<br>
                         <small>
                            ${escapeHtml(
                                client.email
                            )}
                         </small>`
                        :
                        ""
                }

            </td>


            <td>
                ${escapeHtml(
                    client.service || ""
                )}
            </td>


            <td>
                ${escapeHtml(
                    client.invoice_number || ""
                )}
            </td>


            <td>
                $${Number(
                    client.invoice_amount || 0
                ).toLocaleString(
                    "en-US",
                    {
                        minimumFractionDigits: 2,
                        maximumFractionDigits: 2
                    }
                )}
            </td>


            <td>
                ${escapeHtml(
                    formatDate(
                        client.due_date
                    )
                )}
            </td>


            <td>

                <span
                    class="status ${statusClass}">

                    ${escapeHtml(
                        client.status
                    )}

                </span>

            </td>


            <td>

                ${
                    client.drive_folder_url
                    ?
                    `
                    <a
                        href="${escapeAttribute(
                            client.drive_folder_url
                        )}"
                        target="_blank"
                        rel="noopener noreferrer">

                        Open Drive

                    </a>
                    `
                    :
                    `<span style="color:#9ca3af;">
                        Not connected
                     </span>`
                }

            </td>


            <td>

                <button
                    class="btn-primary"
                    onclick="editClient('${client.id}')">

                    Edit

                </button>


                ${
                    currentRole === "admin"
                    ?
                    `
                    <button
                        class="btn-danger"
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


/* =========================================================
   STATUS CLASS
========================================================= */

function getStatusClass(status) {

    switch (status) {

        case "Under Review":
            return "status-under-review";

        case "Pending":
            return "status-pending";

        case "Completed":
            return "status-completed";

        case "Archived":
            return "status-archived";

        case "Overdue":
            return "status-overdue";

        default:
            return "";

    }

}


/* =========================================================
   DATE FORMAT
========================================================= */

function formatDate(dateString) {

    if (!dateString) {
        return "";
    }


    const date =
        new Date(
            dateString + "T00:00:00"
        );


    return date.toLocaleDateString(
        "en-US"
    );

}


/* =========================================================
   OPEN NEW CLIENT
========================================================= */

function openNewClient() {

    document.getElementById(
        "modalTitle"
    ).textContent =
        "Add Client";


    document.getElementById(
        "clientId"
    ).value = "";


    clearForm();


    document.getElementById(
        "clientModal"
    ).style.display = "flex";

}


/* =========================================================
   CLEAR CLIENT FORM
========================================================= */

function clearForm() {

    document.getElementById(
        "companyName"
    ).value = "";


    document.getElementById(
        "contactName"
    ).value = "";


    document.getElementById(
        "clientEmail"
    ).value = "";


    document.getElementById(
        "clientPhone"
    ).value = "";


    document.getElementById(
        "service"
    ).value = "";


    document.getElementById(
        "invoiceNumber"
    ).value = "";


    document.getElementById(
        "invoiceAmount"
    ).value = "";


    document.getElementById(
        "dueDate"
    ).value = "";


    document.getElementById(
        "clientStatus"
    ).value =
        "Under Review";


    document.getElementById(
        "notes"
    ).value = "";


    document.getElementById(
        "driveFolderUrl"
    ).value = "";

}


/* =========================================================
   EDIT CLIENT
========================================================= */

function editClient(id) {

    const client =
        clients.find(
            item =>
                item.id === id
        );


    if (!client) {
        return;
    }


    document.getElementById(
        "modalTitle"
    ).textContent =
        "Edit Client";


    document.getElementById(
        "clientId"
    ).value =
        client.id;


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
        client.invoice_amount || "";


    document.getElementById(
        "dueDate"
    ).value =
        client.due_date || "";


    document.getElementById(
        "clientStatus"
    ).value =
        client.status || "Under Review";


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


/* =========================================================
   SAVE CLIENT
========================================================= */

async function saveClient() {

    const companyName =
        document.getElementById(
            "companyName"
        ).value.trim();


    if (!companyName) {

        alert(
            "Company name is required."
        );

        return;

    }


    if (!currentUser) {

        alert(
            "Your session has expired. Please log in again."
        );

        return;

    }


    const id =
        document.getElementById(
            "clientId"
        ).value;


    const record = {

        company_name:
            companyName,

        contact_name:
            document.getElementById(
                "contactName"
            ).value.trim(),

        email:
            document.getElementById(
                "clientEmail"
            ).value.trim(),

        phone:
            document.getElementById(
                "clientPhone"
            ).value.trim(),

        service:
            document.getElementById(
                "service"
            ).value.trim(),

        invoice_number:
            document.getElementById(
                "invoiceNumber"
            ).value.trim(),

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
            ).value.trim(),

        drive_folder_url:
            document.getElementById(
                "driveFolderUrl"
            ).value.trim(),

        updated_by:
            currentUser.id

    };


    let response;


    if (id) {

        response =
            await supabaseClient
            .from("clients")
            .update(record)
            .eq("id", id);

    } else {

        record.created_by =
            currentUser.id;

        response =
            await supabaseClient
            .from("clients")
            .insert(record);

    }


    if (response.error) {

        alert(
            "Unable to save client: " +
            response.error.message
        );

        return;

    }


    closeModal();

    await loadClients();

}


/* =========================================================
   DELETE CLIENT
========================================================= */

async function deleteClient(id) {

    if (currentRole !== "admin") {

        alert(
            "Only administrators can delete clients."
        );

        return;

    }


    const confirmed =
        confirm(
            "Are you sure you want to permanently delete this client?"
        );


    if (!confirmed) {
        return;
    }


    const { error } =
        await supabaseClient
        .from("clients")
        .delete()
        .eq("id", id);


    if (error) {

        alert(
            "Unable to delete client: " +
            error.message
        );

        return;

    }


    await loadClients();

}


/* =========================================================
   CLOSE MODAL
========================================================= */

function closeModal() {

    document.getElementById(
        "clientModal"
    ).style.display =
        "none";

}


/* =========================================================
   GOOGLE API
========================================================= */

function gapiLoaded() {

    if (
        typeof gapi !== "undefined"
    ) {

        gapi.load(
            "picker",
            () => {
                pickerReady = true;
            }
        );

    }

}


function gisLoaded() {

    if (
        typeof google === "undefined"
    ) {

        return;

    }


    tokenClient =
        google.accounts.oauth2.initTokenClient({

            client_id:
                GOOGLE_CLIENT_ID,

            scope:
                "https://www.googleapis.com/auth/drive.readonly",

            callback: function() {}

        });


    gisReady = true;

}


/* =========================================================
   GOOGLE DRIVE PICKER
========================================================= */

function openDrivePicker() {

    if (!GOOGLE_CLIENT_ID ||
        GOOGLE_CLIENT_ID.includes("YOUR_")) {

        alert(
            "Google Drive has not been configured yet. Add your Google Client ID, API Key, and Project Number to this file."
        );

        return;

    }


    if (
        !pickerReady ||
        !gisReady
    ) {

        alert(
            "Google Drive is still loading. Please try again."
        );

        return;

    }


    tokenClient.callback =
        function(response) {

            if (response.error) {

                console.error(response);

                alert(
                    "Google authorization failed."
                );

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


/* =========================================================
   GOOGLE PICKER CALLBACK
========================================================= */

function pickerCallback(data) {

    if (
        data.action ===
        google.picker.Action.PICKED
    ) {

        const selectedFile =
            data.docs &&
            data.docs[0];


        if (!selectedFile) {
            return;
        }


        document.getElementById(
            "driveFolderUrl"
        ).value =
            selectedFile.url || "";

    }

}


/* =========================================================
   LOGOUT
========================================================= */

async function logout() {

    await supabaseClient.auth.signOut();

    currentUser = null;

    currentRole = null;

    clients = [];

    document
        .getElementById("app")
        .classList.add("hidden");


    document
        .getElementById("loginPage")
        .classList.remove("hidden");


    document.getElementById(
        "email"
    ).value = "";


    document.getElementById(
        "password"
    ).value = "";

}


/* =========================================================
   SECURITY HELPERS
========================================================= */

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
        .replaceAll("&", "&amp;")
        .replaceAll('"', "&quot;")
        .replaceAll("<", "&lt;")
        .replaceAll(">", "&gt;");

}


/* =========================================================
   SESSION CHECK
========================================================= */

supabaseClient.auth.onAuthStateChange(
    async function(event, session) {

        if (
            session &&
            !currentUser
        ) {

            await initializeApp();

        }

    }
);

</script>

</body>
</html>
