digraph FlaskDependencies {

// Graph settings
rankdir=TB;
node [shape=box, style=filled];

// Node definitions with colors
    Main [fillcolor=lightblue, label="Main"];
    FlaskApp [fillcolor=lightgreen, label="Flask App"];
    
// Request handlers
    BeforeRequest [fillcolor=yellow, label="before_request()"];
    AfterRequest [fillcolor=yellow, label="after_request()"];
    
// Database functions
    ConnectDB [fillcolor=orange, label="connect_db()"];
    CheckDB [fillcolor=orange, label="check_db_exists()"];
    QueryDB [fillcolor=orange, label="query_db()"];
    GetUserID [fillcolor=orange, label="get_user_id()"];
    Database [fillcolor=red, shape=cylinder, label="SQLite Database"];
    
// Routes (Web pages)
    SearchPage [fillcolor=lightcyan, label="Search Page (/)"];
    LoginPage [fillcolor=lightcyan, label="Login Page"];
    RegisterPage [fillcolor=lightcyan, label="Register Page"];
    AboutPage [fillcolor=lightcyan, label="About Page"];
    
// API Endpoints
    APISearch [fillcolor=pink, label="API Search"];
    APILogin [fillcolor=pink, label="API Login"];
    APIRegister [fillcolor=pink, label="API Register"];
    APILogout [fillcolor=pink, label="API Logout"];
    
// Security functions
    HashPassword [fillcolor=gold, label="hash_password()"];
    VerifyPassword [fillcolor=gold, label="verify_password()"];
    
// Dependencies
    Main -> FlaskApp;
    Main -> ConnectDB;
    
FlaskApp -> BeforeRequest;
FlaskApp -> AfterRequest;
FlaskApp -> SearchPage;
FlaskApp -> LoginPage;
FlaskApp -> RegisterPage;
FlaskApp -> AboutPage;
FlaskApp -> APISearch;
FlaskApp -> APILogin;
FlaskApp -> APIRegister;
FlaskApp -> APILogout;
    
BeforeRequest -> ConnectDB;
BeforeRequest -> QueryDB;
AfterRequest -> Database;
    
ConnectDB -> CheckDB;
ConnectDB -> Database;
QueryDB -> Database;
GetUserID -> Database;
    
SearchPage -> QueryDB;
    
APISearch -> QueryDB;
    APILogin -> QueryDB;
    APILogin -> VerifyPassword;
    APIRegister -> GetUserID;
    APIRegister -> HashPassword;
    
VerifyPassword -> HashPassword;
    
// Group similar nodes
subgraph cluster_database {
        label="Database Layer";
        color=orange;
        ConnectDB; CheckDB; QueryDB; GetUserID; Database;
    }
    
subgraph cluster_routes {
        label="Web Pages";
        color=lightcyan;
        SearchPage; LoginPage; RegisterPage; AboutPage;
    }
    
subgraph cluster_api {
        label="API Endpoints";
        color=pink;
        APISearch; APILogin; APIRegister; APILogout;
    }
    
subgraph cluster_security {
        label="Security";
        color=gold;
        HashPassword; VerifyPassword;
    }