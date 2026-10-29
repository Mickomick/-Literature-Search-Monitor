<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pharmacovigilance Brand Literature & ICSR Automated Signal System</title>
    <style>
        :root {
            --primary: #0f172a;
            --secondary: #0284c7;
            --accent: #38bdf8;
            --bg-canvas: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #334155;
            --danger: #e11d48;
            --success: #16a34a;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', system-ui, sans-serif; }
        body { background: var(--bg-canvas); color: var(--text-main); display: flex; height: 100vh; overflow: hidden; }
        
        /* Sidebar Navigation */
        aside { width: 290px; background: var(--primary); color: white; display: flex; flex-direction: column; padding: 25px; }
        aside h1 { font-size: 1.15rem; margin-bottom: 6px; color: var(--accent); }
        aside p { font-size: 0.78rem; color: #94a3b8; margin-bottom: 30px; }
        .nav-link { padding: 12px 15px; border-radius: 8px; color: #cbd5e1; text-decoration: none; margin-bottom: 10px; font-weight: 500; transition: 0.2s; display: block; }
        .nav-link:hover, .nav-link.active { background: var(--secondary); color: white; }
        
        /* Main Viewport */
        main { flex: 1; display: flex; flex-direction: column; overflow-y: auto; }
        header { background: white; padding: 20px 30px; border-bottom: 1px solid #e2e8f0; display: flex; justify-content: space-between; align-items: center; }
        .badge { background: #e0f2fe; color: #0369a1; padding: 6px 14px; border-radius: 20px; font-size: 0.8rem; font-weight: 600; }
        
        .dashboard-grid { padding: 30px; display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
        .card { background: var(--card-bg); border-radius: 12px; padding: 25px; box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.08); }
        .card h3 { margin-bottom: 15px; color: var(--primary); font-size: 1.05rem; border-bottom: 2px solid #f1f5f9; padding-bottom: 10px; }
        
        textarea { width: 100%; padding: 12px; border: 1px solid #cbd5e1; border-radius: 8px; margin-bottom: 12px; font-size: 0.88rem; resize: vertical; }
        button { background: var(--secondary); color: white; border: none; padding: 11px 18px; border-radius: 8px; font-weight: 600; cursor: pointer; transition: 0.2s; }
        button:hover { opacity: 0.9; transform: translateY(-1px); }
        .btn-green { background: var(--success); }
        .btn-red { background: var(--danger); }
        
        /* Virtual Pane Terminal Window */
        .virtual-pane { background: #060911; color: #38bdf8; font-family: monospace; padding: 15px; border-radius: 8px; height: 220px; overflow-y: auto; font-size: 0.83rem; line-height: 1.45; }
        
        /* Ticket Data Table */
        .full-span { grid-column: span 2; }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { text-align: left; padding: 12px; border-bottom: 1px solid #e2e8f0; font-size: 0.88rem; }
        th { background: #f8fafc; color: #64748b; }
    </style>
</head>
<body>
    <aside>
        <h1>PV Client Signal Hub</h1>
        <p>Brand Literature & ICSR Workflow</p>
        <a href="#" class="nav-link active">Live Vigilance Panel</a>
        <a href="#" class="nav-link" onclick="pollStream(); return false;">Poll Worldwide Reports</a>
        <a href="#" class="nav-link" onclick="downloadICSRTickets(); return false;">Download QPPV Queue</a>
    </aside>
    
    <main>
        <header>
            <h2>Client-Side Drug Safety Literature Monitor & ICSR Engine</h2>
            <div class="badge" id="sysBadge">System Status: Monitoring | Target: Unique Pharmaceutical Ltd.</div>
        </header>
        
        <div class="dashboard-grid">
            <!-- Module 1: Upload Drug Product Brand Lists -->
            <div class="card">
                <h3>1. Company Drug Brand List Upload Module</h3>
                <p style="font-size: 0.83rem; color: #64748b; margin-bottom: 12px;">Upload comma or line-separated brand product portfolios. Automatically scans online literature matches for Unique Pharmaceutical Limited.</p>
                <textarea id="brandInputBox" rows="4">Aciguard, Lotemp, Haemaron, Uniflox, Unigyl, Exiplon, Unitrim</textarea>
                <button onclick="uploadBrandList()">Update Monitored Brand Portfolio</button>
            </div>
            
            <!-- Module 2: Virtual Pane Worldwide Daily Report Stream -->
            <div class="card">
                <h3>2. Virtual Pane: Worldwide Daily Report Feed</h3>
                <div class="virtual-pane" id="virtualTerminal">
                    [CLIENT SYSTEM INIT] Loaded brand safety libraries for Unique Pharmaceutical Limited.<br>
                    [STREAM] Connected to simulated worldwide drug safety data reporting endpoints.<br>
                    [ACTIVE] Ready to poll daily case feeds and literature mentions...<br>
                    [WATCH] Monitoring brand names for spontaneous adverse reaction disclosures.
                </div>
                <div style="margin-top: 15px; display: flex; justify-content: space-between; align-items: center;">
                    <button class="btn-green" onclick="pollStream()">Poll Worldwide Daily Report Stream</button>
                    <span id="dailyReportCounter" style="font-size: 0.83rem; font-weight: 600; color: #475569;">Worldwide Daily Reports: 4,120</span>
                </div>
            </div>
            
            <!-- Module 3: ICSR Automated Signal Workflow Ticket Queue -->
            <div class="card full-span">
                <h3>3. ICSR Automated Signal Workflow & QPPV Review Queue</h3>
                <p style="font-size: 0.83rem; color: #64748b; margin-bottom: 15px;">Adverse reactions reported online matched by brand name are automatically structured into ICH E2B(R3) ICSR tickets and queued for Qualified Person for Pharmacovigilance (QPPV) medical review.</p>
                <div style="display: flex; gap: 10px; margin-bottom: 15px;">
                    <button onclick="refreshQueueTable()">Refresh Queue</button>
                    <button class="btn-red" onclick="downloadICSRTickets()">Download ICSR Ticket Package (.JSON)</button>
                </div>
                <table>
                    <thead>
                        <tr>
                            <th>Ticket ID</th>
                            <th>Company / Target</th>
                            <th>Suspect Brand Name</th>
                            <th>Drug Safety Data Source</th>
                            <th>Adverse Reaction</th>
                            <th>Severity Level</th>
                            <th>QPPV Status</th>
                        </tr>
                    </thead>
                    <tbody id="ticketTableBody">
                        <tr>
                            <td>ICSR-2026-8819</td>
                            <td>Unique Pharmaceutical Limited</td>
                            <td>Aciguard Suspension</td>
                            <td>Global Drug Safety Feed / MedWatch Online #412</td>
                            <td>Severe Epigastric Burning & Nausea</td>
                            <td><span style="color: #e11d48; font-weight: 600;">Serious (MedDRA SOC: Gastrointestinal disorders)</span></td>
                            <td>Queued for QPPV Medical Review & Sign-off</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </main>

    <script>
        // In-memory data store for the browser session
        let brandCatalog = ["Aciguard", "Lotemp", "Haemaron", "Uniflox", "Unigyl", "Exiplon", "Unitrim", "Paracetamol", "Ibuprofen", "Ciprofloxacin"];
        let dailyCount = 4120;
        let ticketsQueue = [
            {
                ticketId: "ICSR-2026-8819",
                company: "Unique Pharmaceutical Limited",
                brandName: "Aciguard Suspension",
                safetySource: "Global Drug Safety Feed / MedWatch Online #412",
                adverseReaction: "Severe Epigastric Burning & Nausea",
                severity: "Serious (MedDRA SOC: Gastrointestinal disorders)",
                workflowStatus: "Queued for QPPV Medical Review & Sign-off"
            }
        ];

        function logTerminal(text) {
            const terminal = document.getElementById('virtualTerminal');
            terminal.innerHTML += '<br>' + text;
            terminal.scrollTop = terminal.scrollHeight;
        }

        function uploadBrandList() {
            const data = document.getElementById('brandInputBox').value;
            const items = data.split(/[\n,]/);
            let added = 0;
            items.forEach(item => {
                const clean = item.trim();
                if (clean && !brandCatalog.includes(clean)) {
                    brandCatalog.push(clean);
                    added++;
                }
            });
            logTerminal('[CONFIG] Updated brand portfolio successfully. Total active brands: ' + brandCatalog.length);
            alert('Brand product list uploaded successfully! Monitored count: ' + brandCatalog.length);
        }

        function pollStream() {
            logTerminal('[POLL] Querying worldwide daily drug safety data reports & literature...');
            document.getElementById('sysBadge').innerText = 'Status: Polling Worldwide Safety Feeds...';
            
            setTimeout(() => {
                dailyCount += 145;
                const randomId = "ICSR-2026-" + Math.floor(1000 + Math.random() * 9000);
                const newTicket = {
                    ticketId: randomId,
                    company: "Unique Pharmaceutical Limited",
                    brandName: "Lotemp Ophthalmic Solution / Haemaron Syrup",
                    safetySource: "Worldwide Drug Safety Report Feed / PubMed #902",
                    adverseReaction: "Transient Ocular Pruritus & Mild Dizziness",
                    severity: "Non-Serious (MedDRA SOC: Eye / Nervous system disorders)",
                    workflowStatus: "Queued for QPPV Medical Review & Sign-off"
                };
                
                ticketsQueue.unshift(newTicket);
                
                logTerminal('[MATCH] Adverse reaction literature match discovered for Unique Pharmaceutical Limited brand.');
                logTerminal('[WORKFLOW] Generated ICSR automated signal workflow ticket. Queued for QPPV review.');
                document.getElementById('sysBadge').innerText = 'Status: Monitoring | Signal Ticket Queued';
                document.getElementById('dailyReportCounter').innerText = 'Worldwide Daily Reports: ' + dailyCount;
                refreshQueueTable();
            }, 1200);
        }

        function refreshQueueTable() {
            const tbody = document.getElementById('ticketTableBody');
            tbody.innerHTML = '';
            ticketsQueue.forEach(t => {
                tbody.innerHTML += `<tr>
                    <td>${t.ticketId}</td>
                    <td>${t.company}</td>
                    <td>${t.brandName}</td>
                    <td>${t.safetySource}</td>
                    <td>${t.adverseReaction}</td>
                    <td><span style="color: #e11d48; font-weight: 600;">${t.severity}</span></td>
                    <td>${t.workflowStatus}</td>
                </tr>`;
            });
        }

        function downloadICSRTickets() {
            const payload = JSON.stringify(ticketsQueue, null, 2);
            const blob = new Blob([payload], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const anchor = document.createElement('a');
            anchor.href = url;
            anchor.download = 'QPPV_ICSR_Automated_Signal_Tickets_' + new Date().toISOString().slice(0,10) + '.json';
            anchor.click();
            logTerminal('[EXPORT] Downloaded ICSR automated signal tickets package successfully.');
        }
    </script>
</body>
</html>
