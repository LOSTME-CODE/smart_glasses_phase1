<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text-SQL Single Agent - Natural Language SQL Query Generator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1100px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }

        header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 40px 30px;
            text-align: center;
        }

        header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
            font-weight: 700;
        }

        header p {
            font-size: 1.15em;
            opacity: 0.95;
            line-height: 1.5;
        }

        .flex-content {
            display: flex;
            gap: 30px;
        }

        .sidebar {
            flex: 0 0 250px;
            background: #f8f9fa;
            padding: 30px;
            border-right: 1px solid #e0e0e0;
            max-height: 100vh;
            position: sticky;
            top: 0;
            overflow-y: auto;
        }

        .sidebar h3 {
            color: #667eea;
            font-size: 1.1em;
            margin-bottom: 20px;
            font-weight: 600;
        }

        .sidebar ul {
            list-style: none;
        }

        .sidebar li {
            margin-bottom: 10px;
        }

        .sidebar a {
            color: #667eea;
            text-decoration: none;
            font-size: 0.95em;
            transition: all 0.3s ease;
            display: block;
            padding: 8px 12px;
            border-radius: 5px;
        }

        .sidebar a:hover {
            background: #667eea;
            color: white;
            padding-left: 20px;
        }

        .main-content {
            flex: 1;
            padding: 40px;
        }

        section {
            margin-bottom: 50px;
            scroll-margin-top: 100px;
        }

        h2 {
            color: #667eea;
            font-size: 1.8em;
            margin-bottom: 20px;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
        }

        h3 {
            color: #764ba2;
            font-size: 1.3em;
            margin-top: 20px;
            margin-bottom: 15px;
        }

        p {
            margin-bottom: 15px;
            text-align: justify;
            line-height: 1.7;
        }

        .feature-list {
            list-style: none;
            margin: 20px 0;
        }

        .feature-list li {
            padding: 10px 0;
            padding-left: 30px;
            position: relative;
            margin-bottom: 10px;
        }

        .feature-list li:before {
            content: "→";
            position: absolute;
            left: 0;
            color: #667eea;
            font-weight: bold;
            font-size: 1.2em;
        }

        .demo-section {
            background: #f8f9fa;
            padding: 30px;
            border-radius: 8px;
            margin: 30px 0;
        }

        .demo-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }

        .demo-item {
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
        }

        .demo-item:hover {
            transform: translateY(-5px);
        }

        .demo-item img {
            width: 100%;
            height: 250px;
            object-fit: cover;
            background: #f0f0f0;
        }

        .demo-item p {
            padding: 15px;
            margin: 0;
            text-align: center;
            font-size: 0.9em;
        }

        .problem-box {
            background: #fff3cd;
            border-left: 4px solid #ffc107;
            padding: 20px;
            margin: 20px 0;
            border-radius: 5px;
        }

        .problem-box strong {
            color: #856404;
        }

        .solution-box {
            background: #d4edda;
            border-left: 4px solid #28a745;
            padding: 20px;
            margin: 20px 0;
            border-radius: 5px;
        }

        .solution-box strong {
            color: #155724;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            border-radius: 5px;
            overflow: hidden;
        }

        table thead {
            background: #667eea;
            color: white;
        }

        table th {
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }

        table td {
            padding: 12px 15px;
            border-bottom: 1px solid #e0e0e0;
        }

        table tbody tr:nth-child(even) {
            background: #f8f9fa;
        }

        table tbody tr:hover {
            background: #f0f0f0;
            transition: background 0.3s ease;
        }

        .code-block {
            background: #2d2d2d;
            color: #f8f8f2;
            padding: 20px;
            border-radius: 5px;
            overflow-x: auto;
            margin: 20px 0;
            font-family: 'Courier New', monospace;
            font-size: 0.95em;
            line-height: 1.5;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }

        .code-block code {
            color: #f8f8f2;
        }

        .methodology-step {
            background: #f8f9fa;
            border-left: 4px solid #667eea;
            padding: 20px;
            margin: 15px 0;
            border-radius: 5px;
        }

        .step-number {
            display: inline-block;
            background: #667eea;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            text-align: center;
            line-height: 30px;
            font-weight: bold;
            margin-right: 10px;
        }

        .methodology-step strong {
            color: #667eea;
            font-size: 1.05em;
        }

        .result-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 8px;
            margin: 15px 0;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        .result-card strong {
            display: block;
            margin-bottom: 10px;
            font-size: 1.05em;
        }

        .future-features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .future-item {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            font-size: 0.95em;
        }

        footer {
            background: #2d2d2d;
            color: white;
            padding: 30px;
            text-align: center;
            font-size: 0.9em;
        }

        footer a {
            color: #667eea;
            text-decoration: none;
        }

        footer a:hover {
            text-decoration: underline;
        }

        .installation-step {
            background: #f8f9fa;
            padding: 15px;
            margin: 10px 0;
            border-radius: 5px;
            border-left: 4px solid #667eea;
        }

        @media (max-width: 768px) {
            .flex-content {
                flex-direction: column;
            }

            .sidebar {
                flex: none;
                border-right: none;
                border-bottom: 1px solid #e0e0e0;
                position: relative;
                max-height: none;
            }

            header h1 {
                font-size: 1.6em;
            }

            .main-content {
                padding: 20px;
            }

            h2 {
                font-size: 1.4em;
            }

            .demo-grid {
                grid-template-columns: 1fr;
            }

            table {
                font-size: 0.9em;
            }

            table th, table td {
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Text-SQL Single Agent</h1>
            <p>Convert Natural Language Questions into SQL Queries and Get Instant Insights from Databases or CSV Files</p>
        </header>

        <div class="flex-content">
            <!-- Sidebar Navigation -->
            <aside class="sidebar">
                <h3>Table of Contents</h3>
                <ul>
                    <li><a href="#overview">Overview</a></li>
                    <li><a href="#demo">Demo</a></li>
                    <li><a href="#problem-statement">Problem Statement</a></li>
                    <li><a href="#tools-technologies">Tools & Technologies</a></li>
                    <li><a href="#result">Results</a></li>
                    <li><a href="#deployment">Deployment</a></li>
                    <li><a href="#methodology">Methodology</a></li>
                    <li><a href="#future-work">Future Work</a></li>
                </ul>
            </aside>

            <!-- Main Content -->
            <main class="main-content">
                <!-- Overview Section -->
                <section id="overview">
                    <h2>Overview</h2>
                    <p><strong>Text-SQL Single Agent</strong> is an AI-powered data assistant that allows users to interact with structured data using plain English. Instead of writing SQL manually, users can ask questions naturally, and the system automatically generates SQL queries, executes them, and returns results in both raw table format and human-readable summaries.</p>
                    
                    <p>The project includes a user-friendly UI built with Gradio and supports:</p>
                    <ul class="feature-list">
                        <li>SQL Server Databases</li>
                        <li>CSV File Analysis</li>
                    </ul>
                </section>

                <!-- Demo Section -->
                <section id="demo">
                    <h2>Demo</h2>
                    <div class="demo-section">
                        <p style="text-align: center; margin-bottom: 20px;">Check out the application in action:</p>
                        <div class="demo-grid">
                            <div class="demo-item">
                                <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); height: 250px; display: flex; align-items: center; justify-content: center; color: white;">
                                    <span style="font-size: 3em;">▶</span>
                                </div>
                                <p>Video Demo</p>
                            </div>
                            <div class="demo-item">
                                <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); height: 250px; display: flex; align-items: center; justify-content: center; color: white; font-size: 0.9em;">
                                    <span>Query Interface Screenshot</span>
                                </div>
                                <p>Main Application UI</p>
                            </div>
                            <div class="demo-item">
                                <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); height: 250px; display: flex; align-items: center; justify-content: center; color: white; font-size: 0.9em;">
                                    <span>Results Display Screenshot</span>
                                </div>
                                <p>Query Results View</p>
                            </div>
                        </div>
                    </div>
                </section>

                <!-- Problem Statement -->
                <section id="problem-statement">
                    <h2>Problem Statement</h2>
                    <p>Many business users, analysts, and non-technical teams need quick access to data but face significant challenges:</p>
                    
                    <div class="problem-box">
                        <strong>Key Challenges:</strong>
                        <ul class="feature-list" style="margin-top: 15px;">
                            <li>Lack of SQL knowledge among business users</li>
                            <li>Dependency on technical teams for data queries</li>
                            <li>Time-consuming manual query writing</li>
                            <li>Difficulty interpreting raw query results</li>
                            <li>Delayed decision-making due to data access friction</li>
                        </ul>
                    </div>

                    <div class="solution-box">
                        <strong>Our Solution:</strong>
                        <p style="margin: 10px 0;">This project enables <strong>natural language data interaction</strong>, empowering non-technical users to query databases independently and receive actionable insights instantly.</p>
                    </div>
                </section>

                <!-- Tools & Technologies -->
                <section id="tools-technologies">
                    <h2>Tools & Technologies</h2>
                    <table>
                        <thead>
                            <tr>
                                <th>Category</th>
                                <th>Tools Used</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td><strong>Programming Language</strong></td>
                                <td>Python</td>
                            </tr>
                            <tr>
                                <td><strong>User Interface</strong></td>
                                <td>Gradio</td>
                            </tr>
                            <tr>
                                <td><strong>LLM Framework</strong></td>
                                <td>LangChain</td>
                            </tr>
                            <tr>
                                <td><strong>Local Model</strong></td>
                                <td>Ollama (Llama 3.2:3b)</td>
                            </tr>
                            <tr>
                                <td><strong>Primary Database</strong></td>
                                <td>SQL Server</td>
                            </tr>
                            <tr>
                                <td><strong>CSV Engine</strong></td>
                                <td>SQLite (In-Memory)</td>
                            </tr>
                            <tr>
                                <td><strong>Data Handling</strong></td>
                                <td>Pandas</td>
                            </tr>
                            <tr>
                                <td><strong>Query Logic</strong></td>
                                <td>Regex + Prompt Engineering</td>
                            </tr>
                        </tbody>
                    </table>
                </section>

                <!-- Results -->
                <section id="result">
                    <h2>Results</h2>
                    <div class="result-card">
                        <strong>✓ Successfully converts English questions into SQL</strong>
                        Users can ask business questions in natural language and receive accurate SQL-generated results.
                    </div>
                    <div class="result-card">
                        <strong>✓ Works on SQL Server and CSV files</strong>
                        Supports multiple data sources without requiring users to worry about backend complexity.
                    </div>
                    <div class="result-card">
                        <strong>✓ Returns raw + summarized answers</strong>
                        Provides both detailed data tables and human-readable summaries for better understanding.
                    </div>
                    <div class="result-card">
                        <strong>✓ Interactive modern UI experience</strong>
                        Clean, intuitive Gradio interface makes the tool accessible to all technical levels.
                    </div>
                </section>

                <!-- Deployment -->
                <section id="deployment">
                    <h2>Deployment</h2>
                    
                    <h3>Installation</h3>
                    <p>Install required dependencies:</p>
                    <div class="code-block">
                        <code>pip install gradio langchain-ollama langchain-core pyodbc pandas</code>
                    </div>

                    <h3>Setup Ollama Model</h3>
                    <p>Download Ollama and pull the language model:</p>
                    <div class="code-block">
                        <code>ollama pull llama3.2:3b<br>ollama serve</code>
                    </div>

                    <h3>Run the Application</h3>
                    <p>Execute the main script:</p>
                    <div class="code-block">
                        <code>python csvagent5.py</code>
                    </div>

                    <p style="margin-top: 20px; padding: 15px; background: #d4edda; border-radius: 5px; border-left: 4px solid #28a745;">
                        <strong>✓ Success!</strong> The application will start and provide a local URL to access the Gradio interface.
                    </p>
                </section>

                <!-- Methodology -->
                <section id="methodology">
                    <h2>Methodology</h2>
                    <p>The system follows a structured 6-step pipeline to convert natural language queries into executable SQL:</p>

                    <div class="methodology-step">
                        <span class="step-number">1</span>
                        <strong>Input Source Selection</strong>
                        <ul class="feature-list" style="margin-top: 10px;">
                            <li>Connect to SQL Server Database</li>
                            <li>Upload CSV File for analysis</li>
                        </ul>
                    </div>

                    <div class="methodology-step">
                        <span class="step-number">2</span>
                        <strong>Schema Extraction</strong>
                        <ul class="feature-list" style="margin-top: 10px;">
                            <li>Extract table names and structure</li>
                            <li>Identify column names and data types</li>
                            <li>Create schema context for LLM</li>
                        </ul>
                    </div>

                    <div class="methodology-step">
                        <span class="step-number">3</span>
                        <strong>Natural Language to SQL</strong>
                        <p style="margin-top: 10px;"><strong>Process:</strong> User Question → LLM + Schema Context → SQL Query Generation</p>
                        <p style="background: white; padding: 10px; border-radius: 5px; margin-top: 10px; font-style: italic;">
                            <strong>Example:</strong><br>
                            "Show top 5 employees by salary"<br>
                            ↓<br>
                            SELECT TOP 5 name, salary FROM employees ORDER BY salary DESC;
                        </p>
                    </div>

                    <div class="methodology-step">
                        <span class="step-number">4</span>
                        <strong>Query Validation & Safety</strong>
                        <ul class="feature-list" style="margin-top: 10px;">
                            <li>Only SELECT queries allowed</li>
                            <li>No DELETE / UPDATE / DROP operations</li>
                            <li>SQL cleaned and validated before execution</li>
                            <li>Injection attack prevention</li>
                        </ul>
                    </div>

                    <div class="methodology-step">
                        <span class="step-number">5</span>
                        <strong>Query Execution</strong>
                        <ul class="feature-list" style="margin-top: 10px;">
                            <li>Execute validated SQL on SQL Server via pyodbc</li>
                            <li>Handle errors gracefully</li>
                            <li>Return structured result sets</li>
                        </ul>
                    </div>

                    <div class="methodology-step">
                        <span class="step-number">6</span>
                        <strong>NLP Response Generation</strong>
                        <ul class="feature-list" style="margin-top: 10px;">
                            <li>Convert raw database output into readable tables</li>
                            <li>Generate human-friendly text summaries</li>
                            <li>Highlight key insights and patterns</li>
                        </ul>
                    </div>
                </section>

                <!-- Future Work -->
                <section id="future-work">
                    <h2>Future Work</h2>
                    <p>Planned enhancements and features for upcoming versions:</p>
                    
                    <div class="future-features">
                        <div class="future-item">Multi-Database Support</div>
                        <div class="future-item">MySQL, PostgreSQL, Oracle</div>
                        <div class="future-item">Charts & Visualizations</div>
                        <div class="future-item">Export to Excel / PDF</div>
                        <div class="future-item">Voice Query Input</div>
                        <div class="future-item">Authentication & Roles</div>
                        <div class="future-item">Query Optimization</div>
                        <div class="future-item">RAG + SQL Hybrid</div>
                        <div class="future-item">Multi-turn Memory Chat</div>
                        <div class="future-item">Performance Analytics</div>
                    </div>
                </section>
            </main>
        </div>

        <footer>
            <p>&copy; 2024 Text-SQL Single Agent | AI-Powered Data Assistant</p>
            <p style="margin-top: 10px; opacity: 0.7;">Empowering non-technical users to access data with natural language queries</p>
        </footer>
    </div>
</body>
</html>
