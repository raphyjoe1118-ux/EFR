
<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0">

    <title>
        EFR Accounting Firm | Client Dashboard
    </title>


    <!-- ======================================================
         SUPABASE
    ======================================================= -->

    <script
        src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2">
    </script>


    <!-- ======================================================
         GOOGLE IDENTITY SERVICES
         NO GOOGLE API KEY REQUIRED
    ======================================================= -->

    <script
        src="https://accounts.google.com/gsi/client"
        async
        defer>
    </script>


    <style>

        /* =====================================================
           GLOBAL
        ===================================================== */

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
            font-family:
                Arial,
                Helvetica,
                sans-serif;

            background: #f4f6f8;

            color: #1f2937;
        }

        .hidden {
            display: none !important;
        }


        /* =====================================================
           LOGIN
        ===================================================== */

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

            background: #ffffff;

            padding: 40px;

            border-radius: 16px;

            box-shadow:
                0 10px 40px
                rgba(0, 0, 0, .10);

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

            color: white;

            display: flex;

            align-items: center;

            justify-content: center;

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


        /* =====================================================
           HEADER
        ===================================================== */

        .topbar {

            background: #163a5f;

            color: white;

            padding: 18px 30px;

            display: flex;

            align-items: center;

            justify-content: space-between;

            gap: 20px;

            box-shadow:
                0 2px 10px
                rgba(0, 0, 0, .12);

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

            background: white;

            color: #163a5f;

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

        }


        /* =====================================================
           GENERAL
        ===================================================== */

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

            transition: .2s;

        }


        button:hover {

            opacity: .9;

        }


        button:disabled {

            opacity: .5;

            cursor: not-allowed;

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


        /* =====================================================
           DASHBOARD CARDS
        ===================================================== */

        .cards {

            display: grid;

            grid-template-columns:
                repeat(
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

            box-shadow:
                0 2px 10px
                rgba(0, 0, 0, .05);

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


        /* =====================================================
           TOOLBAR
        ===================================================== */

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

        }


        /* =====================================================
           CLIENT TABLE
        ===================================================== */

        .table-container {

            background: white;

            border-radius: 12px;

            overflow-x: auto;

            overflow-y: auto;

            max-height: 65vh;

            min-height: 450px;

            box-shadow:
                0 2px 10px
                rgba(0, 0, 0, .05);

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

            border-bottom:
                1px solid #e5e7eb;

        }


        th {

            background: #1f2937;

            color: white;

            font-size: 13px;

        }


        td {

            font-size: 14px;

            background: white;

        }


        tbody tr:hover td {

            background: #f9fafb;

        }


        /* =====================================================
           STATUS
        ===================================================== */

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


        /* =====================================================
           FORMS
        ===================================================== */

        input,
        select,
        textarea {

            width: 100%;

            padding: 11px 12px;

            border:
                1px solid #d1d5db;

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

            grid-template-columns:
                repeat(2, 1fr);

            gap: 15px;

        }


        .form-grid .full {

            grid-column: 1 / -1;

        }


        /* =====================================================
           MODAL
        ===================================================== */

        .modal {

            display: none;

            position: fixed;

            inset: 0;

            background:
                rgba(0, 0, 0, .50);

            justify-content: center;

            align-items: center;

            padding: 20px;

            z-index: 1000;

        }


        .modal-content {

            background: white;

            width: 100%;

            max-width: 950px;

            max-height: 92vh;

            overflow-y: auto;

            padding: 30px;

            border-radius: 14px;

        }


        .modal-header {

            display: flex;

            justify-content:
                space-between;

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


        /* =====================================================
           GOOGLE DRIVE DOCUMENTS
        ===================================================== */

        .documents-section {

            border:
                1px solid #e5e7eb;

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


        .document-input {

            display: none;

        }


        .documents-list {

            margin-top: 12px;

        }


        .document-item {

            display: flex;

            align-items: center;

            justify-content:
                space-between;

            gap: 12px;

            padding: 11px 12px;

            margin-bottom: 8px;

            background: white;

            border:
                1px solid #e5e7eb;

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

            color: white;

            background: #2563eb;

            padding: 8px 12px;

            border-radius: 6px;

            text-decoration: none;

            font-size: 13px;

        }


        .document-delete {

            background: #dc2626;

            color: white;

            border: none;

            border-radius: 6px;

            padding: 8px 12px;

        }


        .drive-status {

            color: #6b7280;

            font-size: 13px;

            margin-top: 8px;

        }


        .drive-connected {

            background: #ecfdf5;

            color: #166534;

            padding: 10px;

            border-radius: 8px;

            margin-bottom: 10px;

        }


        .drive-file-browser {

            max-height: 320px;

            overflow-y: auto;

            margin-top: 12px;

            border:
                1px solid #e5e7eb;

            border-radius: 8px;

            background: white;

        }


        .drive-file {

            padding: 11px 12px;

            border-bottom:
                1px solid #e5e7eb;

            display: flex;

            justify-content:
                space-between;

            align-items: center;

            gap: 10px;

        }


        .drive-file:last-child {

            border-bottom: none;

        }


        .drive-file-name {

            min-width: 0;

            overflow-wrap: anywhere;

        }


        /* =====================================================
           MESSAGES
        ===================================================== */

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


        /* =====================================================
           MOBILE
        ===================================================== */

        @media (
            max-width: 700px
        ) {

            .topbar {

                flex-direction: column;

                align-items:
                    flex-start;

            }


            .topbar-right {

                width: 100%;

                justify-content:
                    space-between;

            }


            .container {

                padding: 15px;

            }


            .form-grid {

                grid-template-columns:
                    1fr;

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

                flex-direction:
                    column;

                align-items:
                    flex-start;

            }


            .drive-file {

                flex-direction:
                    column;

                align-items:
                    flex-start;

            }

        }

    </style>

</head>


<body>


<!-- ==========================================================
     LOGIN
=========================================================== -->

<div id="loginPage">

    <div class="login-box">

        <div class="login-logo">

            <div class="logo-circle">
                EFR
            </div>


            <h1>
                EFR Accounting Firm
            </h1>


            <p>
                Client Management Portal
            </p>

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


        <div
            id="loginMessage"
            class="message">
        </div>

    </div>

</div>



<!-- ==========================================================
     APPLICATION
=========================================================== -->

<div
    id="app"
    class="hidden">


    <header class="topbar">

        <div class="brand">

            <div class="brand-logo">
                EFR
            </div>


            <div>

                <h2>
                    EFR Accounting Firm
                </h2>


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

                <h4>
                    Total Clients
                </h4>


                <h2
                    id="totalClients">
                    0
                </h2>

            </div>


            <div class="card">

                <h4>
                    Under Review
                </h4>


                <h2
                    id="reviewClients">
                    0
                </h2>

            </div>


            <div class="card">

                <h4>
                    Pending
                </h4>


                <h2
                    id="pendingClients">
                    0
                </h2>

            </div>


            <div class="card">

                <h4>
                    Completed
                </h4>


                <h2
                    id="completedClients">
                    0
                </h2>

            </div>


            <div class="card">

                <h4>
                    Overdue
                </h4>


                <h2
                    id="overdueClients">
                    0
                </h2>

            </div>


            <div class="card">

                <h4>
                    Outstanding
                </h4>


                <h2
                    id="outstanding">
                    $0.00
                </h2>

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

                        <th>
                            Client
                        </th>


                        <th>
                            Contact
                        </th>


                        <th>
                            Service
                        </th>


                        <th>
                            Invoice
                        </th>


                        <th>
                            Amount
                        </th>


                        <th>
                            Due Date
                        </th>


                        <th>
                            Status
                        </th>


                        <th>
                            Documents
                        </th>


                        <th>
                            Actions
                        </th>

                    </tr>

                </thead>


                <tbody
                    id="clientTable">
                </tbody>

            </table>

        </section>

    </main>

</div>



<!-- ==========================================================
     CLIENT MODAL
=========================================================== -->

<div
    id="clientModal"
    class="modal">


    <div
        class="modal-content">


        <div
            class="modal-header">


            <h2
                id="modalTitle">
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


                <select
                    id="clientStatus">

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



            <!-- =================================================
                 GOOGLE DRIVE
            ================================================== -->

            <div
                class="form-group full">


                <div
                    class="documents-section">


                    <label>
                        Google Drive Documents
                    </label>


                    <div
                        id="driveConnectionStatus"
                        class="drive-connected hidden">
                    </div>


                    <div
                        class="documents-toolbar">


                        <button
                            type="button"
                            class="btn-success"
                            onclick="connectGoogleDrive()">

                            Connect Google Drive

                        </button>


                        <button
                            type="button"
                            class="btn-success"
                            onclick="chooseUploadFile()">

                            Upload File

                        </button>


                        <button
                            type="button"
                            class="btn-primary"
                            onclick="showDriveFiles()">

                            Select Existing File

                        </button>


                        <input
                            type="file"
                            id="driveFileInput"
                            class="document-input"
                            onchange="uploadSelectedFile(event)">

                    </div>


                    <div
                        id="driveStatus"
                        class="drive-status">
                    </div>


                    <div
                        id="driveFileBrowser"
                        class="drive-file-browser hidden">
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



        <div
            class="modal-footer">


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


/* ==========================================================
   SUPABASE CONFIGURATION
=========================================================== */

const SUPABASE_URL =
    "https://ujsnwtbdoumtqnnvopti.supabase.co";


const SUPABASE_PUBLISHABLE_KEY =
    "sb_publishable_lXhvukKVSEuQC0UlBPuLg_KNWRxfpW";


const supabaseClient =
    supabase.createClient(

        SUPABASE_URL,

        SUPABASE_PUBLISHABLE_KEY

    );


/* ==========================================================
   GOOGLE OAUTH
   NO GOOGLE API KEY
   NO GOOGLE CLIENT SECRET
=========================================================== */

const GOOGLE_CLIENT_ID =
    "778499336500-v853cm1l21fu82i4g4t85b6urj3t0ap8.apps.googleusercontent.com";


const GOOGLE_DRIVE_SCOPE =
    "https://www.googleapis.com/auth/drive.file";


/* ==========================================================
   STATE
=========================================================== */

let clients = [];

let currentUser = null;

let currentRole = null;

let googleTokenClient = null;

let googleAccessToken = null;


/* ==========================================================
   GOOGLE IDENTITY INITIALIZATION
=========================================================== */

function initializeGoogle() {

    if (
        typeof google ===
        "undefined"
    ) {

        return;

    }


    googleTokenClient =
        google.accounts.oauth2.initTokenClient({

            client_id:
                GOOGLE_CLIENT_ID,

            scope:
                GOOGLE_DRIVE_SCOPE,

            callback:
                function(response) {

                    if (
                        response.error
                    ) {

                        console.error(
                            "Google OAuth error:",
                            response
                        );

                        setDriveStatus(
                            "Google authorization failed: " +
                            (
                                response.error_description ||
                                response.error ||
                                "Unknown error"
                            ),
                            true
                        );

                        return;

                    }


                    googleAccessToken =
                        response.access_token;


                    setDriveConnected(
                        true
                    );


                    setDriveStatus(
                        "Google Drive connected."
                    );


                    /*
                       Refresh the document/file information
                       after authorization.
                    */

                    const clientId =
                        document.getElementById(
                            "clientId"
                        ).value;


                    if (
                        clientId
                    ) {

                        loadClientDocuments(
                            clientId
                        );

                    }

                }

            });

}


window.addEventListener(
    "load",
    function() {

        /*
           Google Identity Services loads asynchronously.
        */

        const waitForGoogle =
            setInterval(
                function() {

                    if (
                        typeof google !==
                        "undefined" &&
                        google.accounts &&
                        google.accounts.oauth2
                    ) {

                        clearInterval(
                            waitForGoogle
                        );

                        initializeGoogle();

                    }

                },
                100
            );


        /*
           Stop checking after 15 seconds.
        */

        setTimeout(
            function() {

                clearInterval(
                    waitForGoogle
                );

            },
            15000
        );

    }
);


/* ==========================================================
   DRIVE UI
=========================================================== */

function setDriveStatus(
    message,
    isError = false
) {

    const element =
        document.getElementById(
            "driveStatus"
        );


    element.textContent =
        message;


    element.className =
        isError
        ?
        "drive-status error"
        :
        "drive-status";

}


function setDriveConnected(
    connected
) {

    const element =
        document.getElementById(
            "driveConnectionStatus"
        );


    if (
        connected
    ) {

        element.textContent =
            "Google Drive is connected for this session.";

        element.classList.remove(
            "hidden"
        );

    } else {

        element.classList.add(
            "hidden"
        );

    }

}


/* ==========================================================
   CONNECT GOOGLE DRIVE
=========================================================== */

function connectGoogleDrive() {

    if (
        !googleTokenClient
    ) {

        /*
           Try one more initialization in case
           Google loaded after the page.
        */

        initializeGoogle();

    }


    if (
        !googleTokenClient
    ) {

        setDriveStatus(
            "Google authorization is still loading. Please try again.",
            true
        );

        return;

    }


    setDriveStatus(
        "Waiting for Google authorization..."
    );


    googleTokenClient.callback =
        function(response) {

            if (
                response.error
            ) {

                console.error(
                    response
                );


                setDriveStatus(

                    "Google authorization failed: " +
                    (
                        response.error_description ||
                        response.error ||
                        "Unknown error"
                    ),

                    true
                );


                return;

            }


            googleAccessToken =
                response.access_token;


            setDriveConnected(
                true
            );


            setDriveStatus(
                "Google Drive connected."
            );


            const clientId =
                document.getElementById(
                    "clientId"
                ).value;


            if (
                clientId
            ) {

                loadClientDocuments(
                    clientId
                );

            }

        };


    googleTokenClient.requestAccessToken({

        prompt:
            googleAccessToken
            ?
            ""
            :
            "consent"

    });

}


/* ==========================================================
   ENSURE GOOGLE TOKEN
=========================================================== */

function ensureGoogleAccess(
    callback
) {

    if (
        googleAccessToken
    ) {

        callback(
            googleAccessToken
        );

        return;

    }


    if (
        !googleTokenClient
    ) {

        initializeGoogle();

    }


    if (
        !googleTokenClient
    ) {

        setDriveStatus(
            "Google authorization is not ready.",
            true
        );

        return;

    }


    googleTokenClient.callback =
        function(response) {

            if (
                response.error
            ) {

                console.error(
                    response
                );


                setDriveStatus(

                    "Google authorization failed: " +
                    (
                        response.error_description ||
                        response.error ||
                        "Unknown error"
                    ),

                    true
                );


                return;

            }


            googleAccessToken =
                response.access_token;


            setDriveConnected(
                true
            );


            callback(
                googleAccessToken
            );

        };


    googleTokenClient.requestAccessToken({

        prompt:
            "consent"

    });

}


/* ==========================================================
   SELECT LOCAL FILE TO UPLOAD
=========================================================== */

function chooseUploadFile() {

    const clientId =
        document.getElementById(
            "clientId"
        ).value;


    if (
        !clientId
    ) {

        alert(
            "Please save the client before uploading documents."
        );

        return;

    }


    ensureGoogleAccess(
        function() {

            document.getElementById(
                "driveFileInput"
            ).click();

        }
    );

}


/* ==========================================================
   UPLOAD FILE TO GOOGLE DRIVE
=========================================================== */

async function uploadSelectedFile(
    event
) {

    const file =
        event.target.files[0];


    if (
        !file
    ) {

        return;

    }


    const clientId =
        document.getElementById(
            "clientId"
        ).value;


    if (
        !clientId
    ) {

        alert(
            "Please save the client first."
        );

        return;

    }


    if (
        !googleAccessToken
    ) {

        alert(
            "Please connect Google Drive first."
        );

        return;

    }


    setDriveStatus(
        "Uploading " +
        file.name +
        " to Google Drive..."
    );


    try {

        /*
           Upload using Google's multipart upload
           endpoint with the user's OAuth token.
        */

        const metadata = {

            name:
                file.name,

            mimeType:
                file.type
                ||
                "application/octet-stream"

        };


        const multipartBody =
            buildMultipartBody(
                metadata,
                file
            );


        const response =
            await fetch(

                "https://www.googleapis.com/upload/drive/v3/files?" +
                "uploadType=multipart&fields=id,name,mimeType,webViewLink",

                {

                    method:
                        "POST",

                    headers: {

                        "Authorization":
                            "Bearer " +
                            googleAccessToken,

                        "Content-Type":
                            multipartBody.contentType

                    },

                    body:
                        multipartBody.body

                }

            );


        /*
           Token expired or revoked.
        */

        if (
            response.status ===
            401
        ) {

            googleAccessToken =
                null;


            setDriveConnected(
                false
            );


            setDriveStatus(
                "Google authorization expired. Please reconnect.",
                true
            );


            return;

        }


        const result =
            await response.json();


        if (
            !response.ok
        ) {

            throw new Error(

                result.error?.message
                ||
                "Google Drive upload failed."

            );

        }


        /*
           Save the Drive file information
           in Supabase.
        */

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
                        result.name
                        ||
                        file.name,

                    file_url:
                        result.webViewLink
                        ||
                        `https://drive.google.com/file/d/${result.id}/view`,

                    google_file_id:
                        result.id,

                    mime_type:
                        result.mimeType
                        ||
                        file.type,

                    uploaded_by:
                        currentUser.id

                });


        if (
            error
        ) {

            throw new Error(
                "Google Drive upload succeeded, " +
                "but Supabase could not save the document: " +
                error.message
            );

        }


        setDriveStatus(
            "Uploaded successfully: " +
            file.name
        );


        await loadClientDocuments(
            clientId
        );


    } catch (
        error
    ) {

        console.error(
            "Drive upload error:",
            error
        );


        setDriveStatus(
            error.message,
            true
        );

    }


    /*
       Reset file input so the same file
       can be selected again.
    */

    event.target.value =
        "";

}


/* ==========================================================
   BUILD MULTIPART BODY
=========================================================== */

function buildMultipartBody(
    metadata,
    file
) {

    const boundary =
        "-------EFRBoundary" +
        Date.now();


    const metadataJson =
        JSON.stringify(
            metadata
        );


    const reader =
        new FileReaderSync();


    /*
       FileReaderSync is only available in
       worker contexts, so we don't use it.
    */

    /*
       Instead create the multipart body with
       Blob objects.
    */

    const body =
        new Blob(

            [

                "--" +
                boundary +
                "\r\n",

                "Content-Type: application/json; charset=UTF-8\r\n",
                "\r\n",

                metadataJson,

                "\r\n",

                "--" +
                boundary +
                "\r\n",

                "Content-Type: " +
                (
                    file.type ||
                    "application/octet-stream"
                ) +
                "\r\n\r\n",

                file,

                "\r\n",

                "--" +
                boundary +
                "--"

            ],

            {
                type:
                    "multipart/related; boundary=" +
                    boundary
            }

        );


    return {

        body:

            body,

        contentType:

            "multipart/related; boundary=" +
            boundary

    };

}


/* ==========================================================
   DRIVE FILE LIST
=========================================================== */

async function showDriveFiles() {

    const clientId =
        document.getElementById(
            "clientId"
        ).value;


    if (
        !clientId
    ) {

        alert(
            "Please save the client first."
        );

        return;

    }


    ensureGoogleAccess(
        async function() {

            await loadDriveFiles();

        }
    );

}


/* ==========================================================
   LOAD DRIVE FILES
=========================================================== */

async function loadDriveFiles() {

    const browser =
        document.getElementById(
            "driveFileBrowser"
        );


    browser.classList.remove(
        "hidden"
    );


    browser.innerHTML = `

        <div
            style="padding:15px;">

            Loading Google Drive files...

        </div>

    `;


    try {

        /*
           Because we use drive.file, this list represents
           files available to the app rather than every file
           in the user's entire Drive.
        */

        const url =
            "https://www.googleapis.com/drive/v3/files?" +

            new URLSearchParams({

                pageSize:
                    "50",

                orderBy:
                    "modifiedTime desc",

                fields:
                    "files(id,name,mimeType,webViewLink,modifiedTime)",

                q:
                    "trashed = false"

            });


        const response =
            await fetch(

                url,

                {

                    headers: {

                        "Authorization":
                            "Bearer " +
                            googleAccessToken

                    }

                }

            );


        if (
            response.status ===
            401
        ) {

            googleAccessToken =
                null;


            setDriveConnected(
                false
            );


            throw new Error(
                "Google authorization expired. Please reconnect."
            );

        }


        const result =
            await response.json();


        if (
            !response.ok
        ) {

            throw new Error(

                result.error?.message
                ||
                "Unable to read Google Drive."

            );

        }


        browser.innerHTML =
            "";


        if (
            !result.files ||
            result.files.length === 0
        ) {

            browser.innerHTML = `

                <div
                    style="padding:15px;">

                    No Drive files are available to this application yet.

                </div>

            `;


            return;

        }


        result.files.forEach(
            file => {

                const row =
                    document.createElement(
                        "div"
                    );


                row.className =
                    "drive-file";


                row.innerHTML = `

                    <div
                        class="drive-file-name">

                        <strong>

                            ${escapeHtml(
                                file.name
                            )}

                        </strong>

                        <br>

                        <small>

                            ${escapeHtml(
                                file.mimeType ||
                                "Google Drive file"
                            )}

                        </small>

                    </div>


                    <button
                        class="btn-primary"
                        onclick="attachExistingDriveFile(
                            '${escapeAttribute(file.id)}',
                            '${escapeAttribute(file.name)}',
                            '${escapeAttribute(file.mimeType || "")}',
                            '${escapeAttribute(
                                file.webViewLink ||
                                `https://drive.google.com/file/d/${file.id}/view`
                            )}'
                        )">

                        Attach

                    </button>

                `;


                browser.appendChild(
                    row
                );

            }
        );


    } catch (
        error
    ) {

        console.error(
            "Drive list error:",
            error
        );


        browser.innerHTML = `

            <div
                style="padding:15px;"
                class="error">

                ${escapeHtml(
                    error.message
                )}

            </div>

        `;

    }

}


/* ==========================================================
   ATTACH EXISTING DRIVE FILE
=========================================================== */

async function attachExistingDriveFile(
    fileId,
    fileName,
    mimeType,
    fileUrl
) {

    const clientId =
        document.getElementById(
            "clientId"
        ).value;


    if (
        !clientId
    ) {

        alert(
            "Please save the client first."
        );

        return;

    }


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
                    mimeType
                    ||
                    null,

                uploaded_by:
                    currentUser.id

            });


    if (
        error
    ) {

        alert(
            "Unable to attach the Drive file:\n\n" +
            error.message
        );

        return;

    }


    setDriveStatus(
        "Drive file attached: " +
        fileName
    );


    await loadClientDocuments(
        clientId
    );

}


/* ==========================================================
   CLIENT LOGIN
=========================================================== */

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


    message.textContent =
        "";


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


/* ==========================================================
   INITIALIZE APP
=========================================================== */

async function initializeApp() {

    const {
        data: {
            user
        }
    } =
        await supabaseClient
            .auth
            .getUser();


    if (
        !user
    ) {

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
        )
        .toLowerCase();


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


/* ==========================================================
   LOAD CLIENTS
=========================================================== */

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


/* ==========================================================
   DASHBOARD
=========================================================== */

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


/* ==========================================================
   RENDER CLIENTS
=========================================================== */

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


    const table =
        document.getElementById(
            "clientTable"
        );


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
                    .filter(
                        Boolean
                    )
                    .join(
                        " "
                    )
                    .toLowerCase();


                return (

                    text.includes(
                        search
                    )

                    &&

                    (
                        !selectedStatus
                        ||
                        client.status ===
                        selectedStatus
                    )

                );

            }
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


/* ==========================================================
   STATUS
=========================================================== */

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


/* ==========================================================
   DATE
=========================================================== */

function formatDate(
    value
) {

    if (
        !value
    ) {

        return "";

    }


    return new Date(
        value +
        "T00:00:00"
    )
    .toLocaleDateString(
        "en-US"
    );

}


/* ==========================================================
   NEW CLIENT
=========================================================== */

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


/* ==========================================================
   CLEAR FORM
=========================================================== */

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

    ]
    .forEach(
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
        "driveFileBrowser"
    ).classList.add(
        "hidden"
    );


    document.getElementById(
        "clientDocuments"
    ).innerHTML = `

        <p class="muted">

            Save the client before adding documents.

        </p>

    `;

}


/* ==========================================================
   EDIT CLIENT
=========================================================== */

async function editClient(
    id
) {

    const client =
        clients.find(
            c =>
                c.id ===
                id
        );


    if (
        !client
    ) {

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


/* ==========================================================
   SAVE CLIENT
=========================================================== */

async function saveClient() {

    if (
        !currentUser
    ) {

        alert(
            "Your login session has expired."
        );


        return;

    }


    const companyName =
        document
            .getElementById(
                "companyName"
            )
            .value
            .trim();


    if (
        !companyName
    ) {

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
            document
                .getElementById(
                    "contactName"
                )
                .value
                .trim(),

        email:
            document
                .getElementById(
                    "clientEmail"
                )
                .value
                .trim(),

        phone:
            document
                .getElementById(
                    "clientPhone"
                )
                .value
                .trim(),

        service:
            document
                .getElementById(
                    "service"
                )
                .value
                .trim(),

        invoice_number:
            document
                .getElementById(
                    "invoiceNumber"
                )
                .value
                .trim(),

        invoice_amount:
            Number(
                document
                    .getElementById(
                        "invoiceAmount"
                    )
                    .value
                    ||
                    0
            ),

        due_date:
            document
                .getElementById(
                    "dueDate"
                )
                .value
                ||
                null,

        status:
            document
                .getElementById(
                    "clientStatus"
                )
                .value,

        notes:
            document
                .getElementById(
                    "notes"
                )
                .value
                .trim(),

        updated_by:
            currentUser.id

    };


    let response;


    if (
        clientId
    ) {

        response =
            await supabaseClient

                .from(
                    "clients"
                )

                .update(
                    record
                )

                .eq(
                    "id",
                    clientId
                );

    } else {

        record.created_by =
            currentUser.id;


        response =
            await supabaseClient

                .from(
                    "clients"
                )

                .insert(
                    record
                );

    }


    if (
        response.error
    ) {

        alert(
            "Unable to save client:\n\n" +
            response.error.message
        );


        return;

    }


    closeModal();

    await loadClients();

}


/* ==========================================================
   LOAD CLIENT DOCUMENTS
=========================================================== */

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

            .from(
                "client_documents"
            )

            .select(
                "*"
            )

            .eq(
                "client_id",
                clientId
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


    container.innerHTML =
        "";


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
                            documentRecord.mime_type
                            ||
                            "Google Drive document"
                        )}

                    </div>

                </div>


                <div
                    class="document-actions">


                    <a
                        href="${escapeAttribute(
                            documentRecord.file_url
                        )}"
                        target="_blank"
                        rel="noopener noreferrer"
                        class="document-link">

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


/* ==========================================================
   VIEW CLIENT DOCUMENTS
=========================================================== */

async function viewClientDocuments(
    clientId
) {

    const client =
        clients.find(
            c =>
                c.id ===
                clientId
        );


    if (
        !client
    ) {

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
        clientId
    );

}


/* ==========================================================
   DELETE DOCUMENT
=========================================================== */

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

            .from(
                "client_documents"
            )

            .delete()

            .eq(
                "id",
                id
            );


    if (
        error
    ) {

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


/* ==========================================================
   DELETE CLIENT
=========================================================== */

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

            .from(
                "clients"
            )

            .delete()

            .eq(
                "id",
                id
            );


    if (
        error
    ) {

        alert(
            "Unable to delete client:\n\n" +
            error.message
        );


        return;

    }


    await loadClients();

}


/* ==========================================================
   CLOSE MODAL
=========================================================== */

function closeModal() {

    document.getElementById(
        "clientModal"
    ).style.display =
        "none";

}


/* ==========================================================
   LOGOUT
=========================================================== */

async function logout() {

    await supabaseClient
        .auth
        .signOut();


    currentUser =
        null;


    currentRole =
        null;


    clients =
        [];


    googleAccessToken =
        null;


    document
        .getElementById(
            "app"
        )
        .classList
        .add(
            "hidden"
        );


    document
        .getElementById(
            "loginPage"
        )
        .classList
        .remove(
            "hidden"
        );


    document.getElementById(
        "email"
    ).value =
        "";


    document.getElementById(
        "password"
    ).value =
        "";

}


/* ==========================================================
   SECURITY HELPERS
=========================================================== */

function escapeHtml(
    value
) {

    return String(
        value
    )

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

    return String(
        value
    )

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


/* ==========================================================
   RESTORE SUPABASE SESSION
=========================================================== */

supabaseClient
    .auth
    .onAuthStateChange(
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
