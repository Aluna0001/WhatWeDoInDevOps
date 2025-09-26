digraph FlaskDependenciesDetailed {
// Graph settings
rankdir=TB;
node [shape=box, style=filled, fontsize=10];
edge [fontsize=8];

    // External Dependencies
    OS [fillcolor=lightsteelblue, label="os module"];
    Sys [fillcolor=lightsteelblue, label="sys module"];
    SQLite3 [fillcolor=lightsteelblue, label="sqlite3 module"];
    Hashlib [fillcolor=lightsteelblue, label="hashlib module"];
    DateTime [fillcolor=lightsteelblue, label="datetime module"];
    ContextLib [fillcolor=lightsteelblue, label="contextlib module"];
    Flask [fillcolor=lightsteelblue, label="Flask framework"];
    
    // Configuration
    Config [fillcolor=wheat, label="Configuration\n(DATABASE_PATH,\nSECRET_KEY, etc.)"];
    
    // Main Flask App
    FlaskApp [fillcolor=lightgreen, label="Flask App Instance"];
    SecretKey [fillcolor=wheat, label="app.secret_key"];
    
    // Global Variables
    GDB [fillcolor=lightyellow, label="g.db\n(request context)"];
    GUser [fillcolor=lightyellow, label="g.user\n(current user)"];
    Session [fillcolor=lightyellow, label="session\n(user_id)"];
    
    // Database Functions
    ConnectDB [fillcolor=orange, label="connect_db()\n(init_mode param)"];
    CheckDB [fillcolor=orange, label="check_db_exists()\n(checks file system)"];
    InitDB [fillcolor=orange, label="init_db()\n(creates tables)"];
    QueryDB [fillcolor=orange, label="query_db()\n(executes SQL)"];
    GetUserID [fillcolor=orange, label="get_user_id()\n(SQL INJECTION!)"];
    Database [fillcolor=red, shape=cylinder, label="SQLite Database\n(../whoknows.db)"];
    SchemaSQL [fillcolor=red, shape=note, label="../schema.sql"];
    
    // Request Lifecycle
    BeforeRequest [fillcolor=yellow, label="@app.before_request\nbefore_request()"];
    AfterRequest [fillcolor=yellow, label="@app.after_request\nafter_request()"];
    
    // Web Page Routes
    SearchRoute [fillcolor=lightcyan, label="@app.route('/')\nsearch()"];
    AboutRoute [fillcolor=lightcyan, label="@app.route('/about')\nabout()"];
    LoginRoute [fillcolor=lightcyan, label="@app.route('/login')\nlogin()"];
    RegisterRoute [fillcolor=lightcyan, label="@app.route('/register')\nregister()"];
    
    // API Routes
    APISearch [fillcolor=pink, label="@app.route('/api/search')\napi_search()\n(SQL INJECTION!)"];
    APILogin [fillcolor=pink, label="@app.route('/api/login')\napi_login()\n(SQL INJECTION!)"];
    APIRegister [fillcolor=pink, label="@app.route('/api/register')\napi_register()\n(SQL INJECTION!)"];
    APILogout [fillcolor=pink, label="@app.route('/api/logout')\nlogout()"];
    
    // Security Functions
    HashPassword [fillcolor=gold, label="hash_password()\n(MD5 - INSECURE!)"];
    VerifyPassword [fillcolor=gold, label="verify_password()\n(compares hashes)"];
    
    // Templates and Responses
    SearchTemplate [fillcolor=lavender, label="search.html\n(with search_results)"];
    AboutTemplate [fillcolor=lavender, label="about.html"];
    LoginTemplate [fillcolor=lavender, label="login.html"];
    RegisterTemplate [fillcolor=lavender, label="register.html"];
    JSONResponse [fillcolor=lavender, label="JSON Response\n(jsonify)"];
    
    // HTTP Request Data
    RequestArgs [fillcolor=mistyrose, label="request.args\n(q, language)"];
    RequestForm [fillcolor=mistyrose, label="request.form\n(username, password, email)"];
    
    // Flask Functions
    RenderTemplate [fillcolor=lightsteelblue, label="render_template()"];
    Redirect [fillcolor=lightsteelblue, label="redirect()"];
    URLFor [fillcolor=lightsteelblue, label="url_for()"];
    Jsonify [fillcolor=lightsteelblue, label="jsonify()"];
    Flash [fillcolor=lightsteelblue, label="flash()"];
    
    // Main Execution
    MainBlock [fillcolor=lightblue, label="if __name__ == '__main__'"];
    AppRun [fillcolor=lightblue, label="app.run()\n(host=0.0.0.0, port=8080)"];
    
    // DEPENDENCIES - External to Internal
    Flask -> FlaskApp [label="creates"];
    Config -> FlaskApp [label="configures"];
    Config -> SecretKey [label="sets"];
    SecretKey -> FlaskApp [label="assigned to"];
    
    // Main execution flow
    MainBlock -> ConnectDB [label="tests connection"];
    MainBlock -> AppRun [label="starts server"];
    AppRun -> FlaskApp [label="runs"];
    
    // Request lifecycle
    FlaskApp -> BeforeRequest [label="triggers before each request"];
    FlaskApp -> AfterRequest [label="triggers after each request"];
    BeforeRequest -> ConnectDB [label="calls"];
    BeforeRequest -> GDB [label="creates"];
    BeforeRequest -> QueryDB [label="calls for user lookup"];
    BeforeRequest -> GUser [label="sets current user"];
    AfterRequest -> GDB [label="closes"];
    
    // Database function dependencies
    ConnectDB -> CheckDB [label="calls (unless init_mode)"];
    ConnectDB -> SQLite3 [label="uses"];
    CheckDB -> OS [label="uses os.path.exists()"];
    CheckDB -> Sys [label="uses sys.exit()"];
    InitDB -> ConnectDB [label="calls with init_mode=True"];
    InitDB -> SchemaSQL [label="reads"];
    InitDB -> ContextLib [label="uses closing()"];
    InitDB -> Database [label="creates tables in"];
    QueryDB -> GDB [label="uses"];
    QueryDB -> Database [label="executes queries on"];
    GetUserID -> GDB [label="uses"];
    GetUserID -> Database [label="queries (VULNERABLE!)"];
    
    // Route dependencies
    FlaskApp -> SearchRoute [label="registers"];
    FlaskApp -> AboutRoute [label="registers"];
    FlaskApp -> LoginRoute [label="registers"];
    FlaskApp -> RegisterRoute [label="registers"];
    FlaskApp -> APISearch [label="registers"];
    FlaskApp -> APILogin [label="registers"];
    FlaskApp -> APIRegister [label="registers"];
    FlaskApp -> APILogout [label="registers"];
    
    // Page route internal dependencies
    SearchRoute -> RequestArgs [label="reads q, language"];
    SearchRoute -> QueryDB [label="calls (VULNERABLE!)"];
    SearchRoute -> RenderTemplate [label="calls"];
    SearchRoute -> SearchTemplate [label="renders"];
    
    AboutRoute -> RenderTemplate [label="calls"];
    AboutRoute -> AboutTemplate [label="renders"];
    
    LoginRoute -> GUser [label="checks"];
    LoginRoute -> URLFor [label="calls"];
    LoginRoute -> Redirect [label="calls"];
    LoginRoute -> RenderTemplate [label="calls"];
    LoginRoute -> LoginTemplate [label="renders"];
    
    RegisterRoute -> GUser [label="checks"];
    RegisterRoute -> URLFor [label="calls"];
    RegisterRoute -> Redirect [label="calls"];
    RegisterRoute -> RenderTemplate [label="calls"];
    RegisterRoute -> RegisterTemplate [label="renders"];
    
    // API route dependencies
    APISearch -> RequestArgs [label="reads q, language"];
    APISearch -> QueryDB [label="calls (VULNERABLE!)"];
    APISearch -> Jsonify [label="calls"];
    APISearch -> JSONResponse [label="returns"];
    
    APILogin -> RequestForm [label="reads username, password"];
    APILogin -> QueryDB [label="calls (VULNERABLE!)"];
    APILogin -> VerifyPassword [label="calls"];
    APILogin -> Flash [label="calls"];
    APILogin -> Session [label="sets user_id"];
    APILogin -> URLFor [label="calls"];
    APILogin -> Redirect [label="calls"];
    APILogin -> RenderTemplate [label="calls on error"];
    APILogin -> LoginTemplate [label="renders on error"];
    
    APIRegister -> GUser [label="checks"];
    APIRegister -> RequestForm [label="reads form data"];
    APIRegister -> GetUserID [label="calls"];
    APIRegister -> HashPassword [label="calls"];
    APIRegister -> GDB [label="uses for INSERT"];
    APIRegister -> Database [label="inserts user (VULNERABLE!)"];
    APIRegister -> Flash [label="calls"];
    APIRegister -> URLFor [label="calls"];
    APIRegister -> Redirect [label="calls"];
    APIRegister -> RenderTemplate [label="calls on error"];
    APIRegister -> RegisterTemplate [label="renders on error"];
    
    APILogout -> Flash [label="calls"];
    APILogout -> Session [label="removes user_id"];
    APILogout -> URLFor [label="calls"];
    APILogout -> Redirect [label="calls"];
    
    // Security function dependencies
    HashPassword -> Hashlib [label="uses hashlib.md5()"];
    VerifyPassword -> HashPassword [label="calls"];
    
    // Critical circular dependencies (dotted lines)
    GUser -> QueryDB [style=dotted, color=red, label="potential circle"];
    Session -> BeforeRequest [style=dotted, color=red, label="session depends on request"];
    
    // Vulnerability indicators
    GetUserID -> Database [color=red, style=bold, label="SQL INJECTION!"];
    APISearch -> QueryDB [color=red, style=bold, label="SQL INJECTION!"];
    APILogin -> QueryDB [color=red, style=bold, label="SQL INJECTION!"];
    APIRegister -> Database [color=red, style=bold, label="SQL INJECTION!"];
    HashPassword -> Hashlib [color=red, style=bold, label="MD5 INSECURE!"];
    
    // Grouping
    subgraph cluster_external {
        label="External Dependencies";
        color=lightsteelblue;
        style=dashed;
        OS; Sys; SQLite3; Hashlib; DateTime; ContextLib; Flask;
        RenderTemplate; Redirect; URLFor; Jsonify; Flash;
    }
    
    subgraph cluster_config {
        label="Configuration";
        color=wheat;
        style=dashed;
        Config; SecretKey;
    }
    
    subgraph cluster_globals {
        label="Global Request Context";
        color=lightyellow;
        style=dashed;
        GDB; GUser; Session;
    }
    
    subgraph cluster_database {
        label="Database Layer (VULNERABLE)";
        color=orange;
        style=solid;
        ConnectDB; CheckDB; InitDB; QueryDB; GetUserID; Database; SchemaSQL;
    }
    
    subgraph cluster_lifecycle {
        label="Request Lifecycle";
        color=yellow;
        style=dashed;
        BeforeRequest; AfterRequest;
    }
    
    subgraph cluster_routes {
        label="Web Page Routes";
        color=lightcyan;
        style=dashed;
        SearchRoute; AboutRoute; LoginRoute; RegisterRoute;
    }
    
    subgraph cluster_api {
        label="API Endpoints (VULNERABLE)";
        color=pink;
        style=solid;
        APISearch; APILogin; APIRegister; APILogout;
    }
    
    subgraph cluster_security {
        label="Security Layer (INSECURE)";
        color=gold;
        style=solid;
        HashPassword; VerifyPassword;
    }
    
    subgraph cluster_templates {
        label="Templates & Responses";
        color=lavender;
        style=dashed;
        SearchTemplate; AboutTemplate; LoginTemplate; RegisterTemplate; JSONResponse;
    }
    
    subgraph cluster_request_data {
        label="Request Data";
        color=mistyrose;
        style=dashed;
        RequestArgs; RequestForm;
    }
    
    subgraph cluster_main {
        label="Main Execution";
        color=lightblue;
        style=dashed;
        MainBlock; AppRun;
    }
}