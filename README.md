
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>EFR Accounting Firm | Client Dashboard</title>

<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

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

html,
body {
    margin: 0;
    padding: 0;
    min-height: 100%;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    background: #f4f6f8;
    color: #1f2937;
}

.hidden {
    display: none !important;
}

/* =========================
   LOGIN
========================= */

#loginPage {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    background: #eef2f7;
}

.login-box {
    width: 100%;
    max-width: 430px;
    background: #fff;
    padding: 40px;
    border-radius: 16px;
    box-shadow: 0 10px 40px rgba(0,0,0,.10);
}

.login-logo {
    text-align: center;
    margin-bottom: 30px;
}

.logo-circle {
    width: 70px;
    height: 70px;
    border-radius: 50%;
    margin: 0 auto 15px;
    background: #163a5f;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 23px;
    font-weight: bold;
}

.login-logo h1 {
    margin: 0;
    color: #163a5f;
    font-size: 28px;
}

.login-logo p {
    color: #6b7280;
    margin-top: 8px;
}

/* =========================
   HEADER
========================= */

.topbar {
    background: #163a5f;
    color: #fff;
    padding: 18px 30px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;
}

.brand {
    display: flex;
    align-items: center;
    gap: 14px;
}

.brand-logo {
    width: 46px;
    height: 46px;
    border-radius: 50%;
    background: #fff;
    color: #163a5f;
    display: flex;
    justify-content: center;
    align-items: center;
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
}

/* =========================
   GENERAL
========================= */

.container {
    max-width: 1500px;
    margin: 0 auto;
    padding: 30px;
}

button {
    border: none;
    border-radius: 7px;
    padding: 10px 15px;
    cursor: pointer;
    font-size: 14px;
}

button:hover {
    opacity: .9;
}

button:disabled {
    opacity: .55;
    cursor: not-allowed;
}

.btn-primary {
    background: #2563eb;
    color: #fff;
}

.btn-danger {
    background: #dc2626;
    color: #fff;
}

.btn-success {
    background: #16a34a;
    color: #fff;
}

.btn-secondary {
    background: #6b7280;
    color: #fff;
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
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    gap: 18px;
    margin-bottom: 25px;
}

.card {
    background: #fff;
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
    background: #fff;
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
}

/* =========================
   CLIENT TABLE
========================= */

.table-container {
    background: #fff;
    border-radius: 12px;
    overflow-x: auto;
    overflow-y: auto;
    max-height: 65vh;
    min-height: 450px;
    box-shadow: 0 2px 10px rgba(0,0,0,.05);
}

.table-container thead th {
    position: sticky;
    top: 0;
    z-index: 5;
    background: #1f2937;
}

table {
    width: 100%;
    border-collapse: collapse;
    min-width: 1200px;
}

th,
td {
    padding: 13px 14px;
    text-align: left;
    border-bottom: 1px solid #e5e7eb;
}

th {
    background: #1f2937;
    color: #fff;
    font-size: 13px;
}

td {
    font-size: 14px;
    background: #fff;
}

tbody tr:hover td {
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
    background: #fff;
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
    background: #fff;
    width: 100%;
    max-width: 900px;
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
    flex-wrap: wrap;
}

/* =========================
   DOCUMENTS
========================= */

.documents-section {
    border: 1px solid #e5e7eb;
    background: #f9fafb;
    border-radius: 10px;
    padding: 16px;
}

.documents-toolbar {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 12px;
}

.documents-list {
    margin-top: 12px;
}

.document-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 12px;
    padding: 11px 12px;
    margin-bottom: 8px;
    background: #fff;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
}

.document-info {
    min-width: 0;
    flex: 1;
}

.document-name {
    font-weight: 600;
    overflow-wrap: anywhere;
}

.document-meta {
    margin-top: 4px;
    color: #6b7280;
    font-size: 12px;
}

.document-actions {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
}

.document-link {
    display: inline-block;
    color: #fff;
    background: #2563eb;
    padding: 8px 12px;
    border-radius: 6px;
    text-decoration: none;
    font-size: 13px;
}

.document-delete {
    background: #dc2626;
    color: #fff;
    border: none;
    border-radius: 6px;
    padding: 8px 12px;
}

.drive-status {
    color: #6b7280;
    font-size: 13px;
    margin-top: 8px;
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

.muted {
    color: #9ca3af;
}

.empty-state {
    text-align: center;
    padding: 50px;
    color: #6b7280;
}

a {
    color: #2563eb;
}

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

    .table-container {
        max-height: 70vh;
        min-height: 400px;
    }

    .modal-content {
        padding: 20px;
    }

    .document-item {
        flex-direction: column;
        align-items: flex-start;
    }
}

</style>
</head>

<body>

<!-- =========================================================
     LOGIN
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
                autocomplete="username">

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

            Sign In

        </button>

        <div id="loginMessage" class="message"></div>

    </div>

</div>


<!-- =========================================================
     APPLICATION
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


        <!-- SEARCH -->

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

                <option>Under Review</option>
                <option>Pending</option>
                <option>Completed</option>
                <option>Archived</option>
                <option>Overdue</option>

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
                        <th>Documents</th>
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

<div id="clientModal" class="modal">

    <div class="modal-content">

        <div class="modal-header">

            <h2 id="modalTitle">
                Add Client
            </h2>

            <button
                class="btn-light"
                onclick="closeModal()">

                X

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
                    min="0"
                    step="0.01"
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

                    <option>Under Review</option>
                    <option>Pending</option>
                    <option>Completed</option>
                    <option>Archived</option>
                    <option>Overdue</option>

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


            <!-- DOCUMENTS -->

            <div class="form-group full">

                <div class="documents-section">

                    <label>
                        Client Documents
                    </label>

                    <div class="documents-toolbar">

                        <button
                            type="button"
                            class="btn-success"
                            onclick="openDriveUploadPicker()">

                            Upload to Google Drive

                        </button>

                        <button
                            type="button"
                            class="btn-primary"
                            onclick="openDriveSelectPicker()">

                            Select Existing File

                        </button>

                    </div>

                    <div
                        id="driveStatus"
                        class="drive-status">
                    </div>

                    <div
                        id="clientDocuments"
                        class="documents-list">

                        <p class="muted">
                            Save the client before adding documents.
                        </p>

                    </div>

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
   SUPABASE
========================================================= */

const SUPABASE_URL =
    "https://ujsnwtbdoumtqnnvopti.supabase.co";

const SUPABASE_PUBLISHABLE_KEY =
    "sb_publishable_lXhvukwKVSEuQC0UlBPuLg_KNWRxfpW";

const supabaseClient =
    supabase.createClient(
        SUPABASE_URL,
        SUPABASE_PUBLISHABLE_KEY
    );


/* =========================================================
   GOOGLE CLOUD
========================================================= */

const GOOGLE_CLIENT_ID =
    "778499336500-v853cm1l21fu82i4g4t85b6urj3t0ap8.apps.googleusercontent.com";

const GOOGLE_API_KEY =
    "AIzaSyAt3-jtz0k-jgR2t3_QLeZAo3A6hz1cdmE";

const GOOGLE_APP_ID =
    "778499336500";

const GOOGLE_DRIVE_SCOPE =
    "https://www.googleapis.com/auth/drive.file";


/* =========================================================
   STATE
========================================================= */

let clients = [];

let currentUser = null;

let currentRole = null;

let tokenClient = null;

let accessToken = null;

let pickerReady = false;

let gisReady = false;


/* =========================================================
   GOOGLE INITIALIZATION
========================================================= */

function gapiLoaded() {

    if (typeof gapi === "undefined") {

        console.error(
            "Google API library did not load."
        );

        return;
    }

    gapi.load(
        "picker",
        function() {

            pickerReady = true;

            console.log(
                "Google Picker loaded."
            );

        }
    );
}


function gisLoaded() {

    if (
        typeof google === "undefined"
    ) {

        console.error(
            "Google Identity Services did not load."
        );

        return;
    }

    tokenClient =
        google.accounts.oauth2.initTokenClient({

            client_id:
                GOOGLE_CLIENT_ID,

            scope:
                GOOGLE_DRIVE_SCOPE,

            callback:
                function() {}

        });

    gisReady = true;

    console.log(
        "Google Identity Services loaded."
    );
}


/* =========================================================
   GOOGLE AUTH
========================================================= */

function authorizeGoogleDrive(
    callback
) {

    if (!pickerReady) {

        alert(
            "Google Picker has not finished loading. " +
            "Please refresh the page and try again."
        );

        return;
    }

    if (!gisReady || !tokenClient) {

        alert(
            "Google authentication has not finished loading. " +
            "Please refresh the page and try again."
        );

        return;
    }

    tokenClient.callback =
        function(response) {

            if (
                response.error
            ) {

                console.error(
                    "Google OAuth error:",
                    response
                );

                alert(
                    "Google Drive authorization failed.\n\n" +
                    "Error: " +
                    (
                        response.error ||
                        "Unknown Google authorization error"
                    )
                );

                return;
            }

            accessToken =
                response.access_token;

            callback();
        };


    tokenClient.requestAccessToken({

        prompt:
            accessToken
            ? ""
            : "consent"

    });

}


/* =========================================================
   UPLOAD TO GOOGLE DRIVE
========================================================= */

function openDriveUploadPicker() {

    authorizeGoogleDrive(
        function() {

            const clientId =
                document.getElementById(
                    "clientId"
                ).value;

            if (!clientId) {

                alert(
                    "Please save the client first."
                );

                return;
            }


            const uploadView =
                new google.picker.DocsUploadView();


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

                    .addView(
                        uploadView
                    )

                    .setCallback(
                        drivePickerCallback
                    )

                    .build();


            picker.setVisible(
                true
            );

        }
    );

}


/* =========================================================
   SELECT EXISTING DRIVE FILE
========================================================= */

function openDriveSelectPicker() {

    authorizeGoogleDrive(
        function() {

            const clientId =
                document.getElementById(
                    "clientId"
                ).value;

            if (!clientId) {

                alert(
                    "Please save the client first."
                );

                return;
            }


            const docsView =
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

                    .addView(
                        docsView
                    )

                    .setCallback(
                        drivePickerCallback
                    )

                    .build();


            picker.setVisible(
                true
            );

        }
    );

}


/* =========================================================
   PICKER CALLBACK
========================================================= */

async function drivePickerCallback(
    data
) {

    if (
        data.action !==
        google.picker.Action.PICKED
    ) {

        return;
    }


    const selectedDocuments =
        data[
            google.picker.Response.DOCUMENTS
        ];


    if (
        !selectedDocuments ||
        selectedDocuments.length === 0
    ) {

        return;
    }


    const clientId =
        document.getElementById(
            "clientId"
        ).value;


    if (!clientId) {

        alert(
            "Please save the client before adding documents."
        );

        return;
    }


    document.getElementById(
        "driveStatus"
    ).textContent =
        "Adding document(s)...";


    let addedCount = 0;


    for (
        const selected of selectedDocuments
    ) {

        const fileId =
            selected[
                google.picker.Document.ID
            ];


        const fileName =
            selected[
                google.picker.Document.NAME
            ]
            ||
            "Google Drive File";


        const fileUrl =
            selected.url
            ||
            `https://drive.google.com/file/d/${fileId}/view`;


        const mimeType =
            selected[
                google.picker.Document.MIME_TYPE
            ]
            ||
            null;


        const {
            error
        } =
            await supabaseClient

                .from(
                    "client_documents"
                )

                .insert({

                    client_id:
                        clientId,

                    file_name:
                        fileName,

                    file_url:
                        fileUrl,

                    google_file_id:
                        fileId,

                    mime_type:
                        mimeType,

                    uploaded_by:
                        currentUser.id

                });


        if (
            error
        ) {

            console.error(
                "Document save error:",
                error
            );

            alert(
                "Google Drive selected the file, " +
                "but Supabase could not save it:\n\n" +
                error.message
            );

            continue;
        }


        addedCount++;
    }


    document.getElementById(
        "driveStatus"
    ).textContent =
        addedCount +
        " document(s) added.";


    await loadClientDocuments(
        clientId
    );

}


/* =========================================================
   LOGIN
========================================================= */

async function login() {

    const email =
        document.getElementById(
            "email"
        )
        .value
        .trim();


    const password =
        document.getElementById(
            "password"
        )
        .value;


    const message =
        document.getElementById(
            "loginMessage"
        );


    message.textContent = "";

    message.className =
        "message";


    if (
        !email ||
        !password
    ) {

        message.textContent =
            "Please enter your email and password.";

        message.classList.add(
            "error"
        );

        return;
    }


    try {

        const {
            data,
            error
        } =
            await supabaseClient
                .auth
                .signInWithPassword({

                    email,
                    password

                });


        if (
            error
        ) {

            message.textContent =
                "Login failed: " +
                error.message;

            message.classList.add(
                "error"
            );

            return;
        }


        currentUser =
            data.user;


        await initializeApp();

    } catch (
        error
    ) {

        message.textContent =
            "Login failed: " +
            (
                error.message ||
                "Unexpected error."
            );

        message.classList.add(
            "error"
        );

    }
}


/* =========================================================
   INITIALIZE
========================================================= */

async function initializeApp() {

    const {
        data: {
            user
        }
    } =
        await supabaseClient
            .auth
            .getUser();


    if (!user) {

        return;
    }


    currentUser =
        user;


    const {
        data: roleData,
        error
    } =
        await supabaseClient

            .from(
                "user_roles"
            )

            .select(
                "role"
            )

            .eq(
                "user_id",
                user.id
            )

            .single();


    if (
        error ||
        !roleData
    ) {

        alert(
            "This account does not have an EFR Accounting Firm role assigned."
        );


        await supabaseClient
            .auth
            .signOut();


        return;
    }


    currentRole =
        String(
            roleData.role
        ).toLowerCase();


    if (
        currentRole ===
        "staff"
    ) {

        currentRole =
            "client";

    }


    document
        .getElementById(
            "loginPage"
        )
        .classList
        .add(
            "hidden"
        );


    document
        .getElementById(
            "app"
        )
        .classList
        .remove(
            "hidden"
        );


    document
        .getElementById(
            "userRole"
        )
        .textContent =
            "Signed in as " +
            currentRole.toUpperCase();


    await loadClients();

}


/* =========================================================
   LOAD CLIENTS
========================================================= */

async function loadClients() {

    const {
        data,
        error
    } =
        await supabaseClient

            .from(
                "clients"
            )

            .select(
                "*"
            )

            .order(
                "created_at",
                {
                    ascending:
                        false
                }
            );


    if (
        error
    ) {

        alert(
            "Unable to load clients:\n\n" +
            error.message
        );

        return;
    }


    clients =
        data ||
        [];


    updateDashboard();

    renderClients();

}


/* =========================================================
   DASHBOARD
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
            c =>
                c.status ===
                "Under Review"
        ).length;


    document.getElementById(
        "pendingClients"
    ).textContent =
        clients.filter(
            c =>
                c.status ===
                "Pending"
        ).length;


    document.getElementById(
        "completedClients"
    ).textContent =
        clients.filter(
            c =>
                c.status ===
                "Completed"
        ).length;


    document.getElementById(
        "overdueClients"
    ).textContent =
        clients.filter(
            c =>
                c.status ===
                "Overdue"
        ).length;


    const outstanding =
        clients
            .filter(
                c =>
                    c.status !==
                    "Completed"
            )
            .reduce(
                (
                    total,
                    c
                ) =>
                    total +
                    Number(
                        c.invoice_amount ||
                        0
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
                minimumFractionDigits:
                    2,
                maximumFractionDigits:
                    2
            }
        );
}


/* =========================================================
   RENDER CLIENTS
========================================================= */

function renderClients() {

    const search =
        document.getElementById(
            "search"
        )
        .value
        .toLowerCase()
        .trim();


    const selectedStatus =
        document.getElementById(
            "statusFilter"
        ).value;


    const filtered =
        clients.filter(
            client => {

                const text =
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


                return (
                    text.includes(search) &&
                    (
                        !selectedStatus ||
                        client.status ===
                        selectedStatus
                    )
                );

            }
        );


    const table =
        document.getElementById(
            "clientTable"
        );


    table.innerHTML =
        "";


    if (
        filtered.length ===
        0
    ) {

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


    filtered.forEach(
        client => {

            const row =
                document.createElement(
                    "tr"
                );


            row.innerHTML = `

                <td>

                    <strong>

                        ${escapeHtml(
                            client.company_name ||
                            ""
                        )}

                    </strong>

                </td>


                <td>

                    ${escapeHtml(
                        client.contact_name ||
                        ""
                    )}

                    ${
                        client.email
                        ?
                        `
                        <br>

                        <small>

                            ${escapeHtml(
                                client.email
                            )}

                        </small>
                        `
                        :
                        ""
                    }

                </td>


                <td>
                    ${escapeHtml(
                        client.service ||
                        ""
                    )}
                </td>


                <td>
                    ${escapeHtml(
                        client.invoice_number ||
                        ""
                    )}
                </td>


                <td>

                    $${Number(
                        client.invoice_amount ||
                        0
                    ).toLocaleString(
                        "en-US",
                        {
                            minimumFractionDigits:
                                2,
                            maximumFractionDigits:
                                2
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
                        class="status ${getStatusClass(
                            client.status
                        )}">

                        ${escapeHtml(
                            client.status
                        )}

                    </span>

                </td>


                <td>

                    <button
                        class="btn-primary"
                        onclick="viewClientDocuments(
                            '${client.id}'
                        )">

                        Documents

                    </button>

                </td>


                <td>

                    <button
                        class="btn-primary"
                        onclick="editClient(
                            '${client.id}'
                        )">

                        Edit

                    </button>


                    ${
                        currentRole ===
                        "admin"

                        ?

                        `
                        <button
                            class="btn-danger"
                            onclick="deleteClient(
                                '${client.id}'
                            )">

                            Delete

                        </button>
                        `

                        :

                        ""
                    }

                </td>

            `;


            table.appendChild(
                row
            );

        }
    );
}


/* =========================================================
   STATUS CLASS
========================================================= */

function getStatusClass(
    status
) {

    switch (
        status
    ) {

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
   DATE
========================================================= */

function formatDate(
    value
) {

    if (!value) {
        return "";
    }


    return new Date(
        value + "T00:00:00"
    ).toLocaleDateString(
        "en-US"
    );
}


function formatDateTime(
    value
) {

    if (!value) {
        return "";
    }


    return new Date(
        value
    ).toLocaleString(
        "en-US"
    );
}


/* =========================================================
   NEW CLIENT
========================================================= */

function openNewClient() {

    document.getElementById(
        "modalTitle"
    ).textContent =
        "Add Client";


    document.getElementById(
        "clientId"
    ).value =
        "";


    clearForm();


    document.getElementById(
        "clientModal"
    ).style.display =
        "flex";

}


/* =========================================================
   CLEAR FORM
========================================================= */

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
        "notes"

    ].forEach(
        id => {

            document.getElementById(
                id
            ).value =
                "";

        }
    );


    document.getElementById(
        "clientStatus"
    ).value =
        "Under Review";


    document.getElementById(
        "driveStatus"
    ).textContent =
        "";


    document.getElementById(
        "clientDocuments"
    ).innerHTML = `

        <p class="muted">

            Save the client before adding documents.

        </p>

    `;
}


/* =========================================================
   EDIT CLIENT
========================================================= */

async function editClient(
    id
) {

    const client =
        clients.find(
            c =>
                c.id ===
                id
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
        client.company_name ||
        "";


    document.getElementById(
        "contactName"
    ).value =
        client.contact_name ||
        "";


    document.getElementById(
        "clientEmail"
    ).value =
        client.email ||
        "";


    document.getElementById(
        "clientPhone"
    ).value =
        client.phone ||
        "";


    document.getElementById(
        "service"
    ).value =
        client.service ||
        "";


    document.getElementById(
        "invoiceNumber"
    ).value =
        client.invoice_number ||
        "";


    document.getElementById(
        "invoiceAmount"
    ).value =
        client.invoice_amount ||
        "";


    document.getElementById(
        "dueDate"
    ).value =
        client.due_date ||
        "";


    document.getElementById(
        "clientStatus"
    ).value =
        client.status ||
        "Under Review";


    document.getElementById(
        "notes"
    ).value =
        client.notes ||
        "";


    document.getElementById(
        "clientModal"
    ).style.display =
        "flex";


    await loadClientDocuments(
        client.id
    );

}


/* =========================================================
   SAVE CLIENT
========================================================= */

async function saveClient() {

    if (!currentUser) {

        alert(
            "Your login session has expired."
        );

        return;
    }


    const companyName =
        document.getElementById(
            "companyName"
        )
        .value
        .trim();


    if (!companyName) {

        alert(
            "Company name is required."
        );

        return;
    }


    const clientId =
        document.getElementById(
            "clientId"
        ).value;


    const record = {

        company_name:
            companyName,

        contact_name:
            document.getElementById(
                "contactName"
            )
            .value
            .trim(),

        email:
            document.getElementById(
                "clientEmail"
            )
            .value
            .trim(),

        phone:
            document.getElementById(
                "clientPhone"
            )
            .value
            .trim(),

        service:
            document.getElementById(
                "service"
            )
            .value
            .trim(),

        invoice_number:
            document.getElementById(
                "invoiceNumber"
            )
            .value
            .trim(),

        invoice_amount:
            Number(
                document.getElementById(
                    "invoiceAmount"
                )
                .value ||
                0
            ),

        due_date:
            document.getElementById(
                "dueDate"
            )
            .value ||
            null,

        status:
            document.getElementById(
                "clientStatus"
            )
            .value,

        notes:
            document.getElementById(
                "notes"
            )
            .value
            .trim(),

        updated_by:
            currentUser.id

    };


    let response;


    if (clientId) {

        response =
            await supabaseClient
                .from("clients")
                .update(record)
                .eq("id", clientId);

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
            "Unable to save client:\n\n" +
            response.error.message
        );

        return;
    }


    closeModal();

    await loadClients();

}


/* =========================================================
   LOAD CLIENT DOCUMENTS
========================================================= */

async function loadClientDocuments(
    clientId
) {

    const container =
        document.getElementById(
            "clientDocuments"
        );


    container.innerHTML = `

        <p class="muted">
            Loading documents...
        </p>

    `;


    const {
        data,
        error
    } =
        await supabaseClient
            .from("client_documents")
            .select("*")
            .eq("client_id", clientId)
            .order(
                "created_at",
                {
                    ascending:
                        false
                }
            );


    if (error) {

        container.innerHTML = `

            <p class="error">

                ${escapeHtml(
                    error.message
                )}

            </p>

        `;

        return;
    }


    if (
        !data ||
        data.length === 0
    ) {

        container.innerHTML = `

            <p class="muted">
                No documents attached.
            </p>

        `;

        return;
    }


    container.innerHTML = "";


    data.forEach(
        documentRecord => {

            const item =
                document.createElement(
                    "div"
                );


            item.className =
                "document-item";


            item.innerHTML = `

                <div
                    class="document-info">

                    <div
                        class="document-name">

                        ${escapeHtml(
                            documentRecord.file_name
                        )}

                    </div>

                    <div
                        class="document-meta">

                        ${escapeHtml(
                            documentRecord.mime_type ||
                            "Google Drive document"
                        )}

                        ${
                            documentRecord.created_at
                            ?
                            " • Added " +
                            escapeHtml(
                                formatDateTime(
                                    documentRecord.created_at
                                )
                            )
                            :
                            ""
                        }

                    </div>

                </div>


                <div
                    class="document-actions">

                    <a
                        class="document-link"
                        href="${escapeAttribute(
                            documentRecord.file_url
                        )}"
                        target="_blank"
                        rel="noopener noreferrer">

                        Open

                    </a>


                    ${
                        currentRole ===
                        "admin"

                        ?

                        `
                        <button
                            class="document-delete"
                            onclick="deleteDocument(
                                '${documentRecord.id}'
                            )">

                            Delete

                        </button>
                        `

                        :

                        ""
                    }

                </div>

            `;


            container.appendChild(
                item
            );

        }
    );
}


/* =========================================================
   VIEW CLIENT DOCUMENTS
========================================================= */

async function viewClientDocuments(
    clientId
) {

    const client =
        clients.find(
            c =>
                c.id ===
                clientId
        );


    if (!client) {
        return;
    }


    document.getElementById(
        "modalTitle"
    ).textContent =
        "Client Documents — " +
        client.company_name;


    document.getElementById(
        "clientId"
    ).value =
        client.id;


    document.getElementById(
        "companyName"
    ).value =
        client.company_name ||
        "";


    document.getElementById(
        "contactName"
    ).value =
        client.contact_name ||
        "";


    document.getElementById(
        "clientEmail"
    ).value =
        client.email ||
        "";


    document.getElementById(
        "clientPhone"
    ).value =
        client.phone ||
        "";


    document.getElementById(
        "service"
    ).value =
        client.service ||
        "";


    document.getElementById(
        "invoiceNumber"
    ).value =
        client.invoice_number ||
        "";


    document.getElementById(
        "invoiceAmount"
    ).value =
        client.invoice_amount ||
        "";


    document.getElementById(
        "dueDate"
    ).value =
        client.due_date ||
        "";


    document.getElementById(
        "clientStatus"
    ).value =
        client.status ||
        "Under Review";


    document.getElementById(
        "notes"
    ).value =
        client.notes ||
        "";


    document.getElementById(
        "clientModal"
    ).style.display =
        "flex";


    await loadClientDocuments(
        client.id
    );

}


/* =========================================================
   DELETE DOCUMENT
========================================================= */

async function deleteDocument(
    id
) {

    if (
        currentRole !==
        "admin"
    ) {

        alert(
            "Only an administrator can delete documents."
        );

        return;
    }


    if (
        !confirm(
            "Remove this document from the client record?"
        )
    ) {

        return;
    }


    const {
        error
    } =
        await supabaseClient
            .from("client_documents")
            .delete()
            .eq("id", id);


    if (error) {

        alert(
            "Unable to remove document:\n\n" +
            error.message
        );

        return;
    }


    const clientId =
        document.getElementById(
            "clientId"
        ).value;


    await loadClientDocuments(
        clientId
    );
}


/* =========================================================
   DELETE CLIENT
========================================================= */

async function deleteClient(
    id
) {

    if (
        currentRole !==
        "admin"
    ) {

        alert(
            "Only an administrator can delete clients."
        );

        return;
    }


    if (
        !confirm(
            "Are you sure you want to permanently delete this client?"
        )
    ) {

        return;
    }


    const {
        error
    } =
        await supabaseClient
            .from("clients")
            .delete()
            .eq("id", id);


    if (error) {

        alert(
            "Unable to delete client:\n\n" +
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
   LOGOUT
========================================================= */

async function logout() {

    await supabaseClient.auth.signOut();


    currentUser = null;
    currentRole = null;
    clients = [];


    document
        .getElementById("app")
        .classList
        .add("hidden");


    document
        .getElementById("loginPage")
        .classList
        .remove("hidden");


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

function escapeHtml(
    value
) {

    return String(value)
        .replaceAll(
            "&",
            "&amp;"
        )
        .replaceAll(
            "<",
            "&lt;"
        )
        .replaceAll(
            ">",
            "&gt;"
        )
        .replaceAll(
            '"',
            "&quot;"
        )
        .replaceAll(
            "'",
            "&#039;"
        );

}


function escapeAttribute(
    value
) {

    return String(value)
        .replaceAll(
            "&",
            "&amp;"
        )
        .replaceAll(
            '"',
            "&quot;"
        )
        .replaceAll(
            "<",
            "&lt;"
        )
        .replaceAll(
            ">",
            "&gt;"
        );

}


/* =========================================================
   RESTORE SESSION
========================================================= */

supabaseClient.auth.onAuthStateChange(
    async function(
        event,
        session
    ) {

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
