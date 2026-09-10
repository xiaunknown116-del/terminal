import React, { useState, useEffect } from 'react';import {Activity, Server, Database, ShieldAlert, Cpu, HardDrive, Wifi, Search, Filter,RefreshCw, Download, ChevronDown, CheckCircle2, AlertTriangle, XCircle, Terminal,Layers, ArrowUpRight, ArrowDownRight, BookOpen, FileText, Settings, Code,ShieldCheck, Share2, HelpCircle, Link, Sliders, ShieldX, UserCheck, AlertCircle,Rss, Globe, Mail, Shield, TrendingUp, Percent, Coins, Scale, Key, Lock, Unlock, Zap,CreditCard, Building2, BadgeCheck, Briefcase} from 'lucide-react';export default function App() {// Navigation & Core Operational View Stateconst [activeTab, setActiveTab] = useState('cloudflare');const [isLiveStream, setIsLiveStream] = useState(true);const [viewXmlMode, setViewXmlMode] = useState(false);const [notification, setNotification] = useState(null);// Salesforce Admin Connector Troubleshooting Stateconst [salesforceConnectorStatus, setSalesforceConnectorStatus] = useState('OAUTH_ERROR');const [isAdminApproved, setIsAdminApproved] = useState(false);const [isMfaVerified, setIsMfaVerified] = useState(false);const [mfaInputCode, setMfaInputCode] = useState('');const [mfaError, setMfaError] = useState('');const [salesforceLogs, setSalesforceLogs] = useState([{ timestamp: '10:30:15', type: 'ERROR', message: 'OAuth handshake failed: invalid_grant_signature' },{ timestamp: '10:31:02', type: 'WARN', message: 'Retrying connection via primary gateway cluster...' },{ timestamp: '10:32:40', type: 'INFO', message: 'Awaiting Administrator authorization multi-sign override' }]);// Identity & KYC Connector State (Persona / Veriff)const [identityProviders, setIdentityProviders] = useState([{ id: 'persona-01', name: 'Persona Inquiry Webhook', type: 'KYC/AML Ingress', status: 'ACTIVE', verifiedToday: 142, flaggedCount: 2, avgLatency: '1.2s' },{ id: 'veriff-02', name: 'Veriff Biometric SDK', type: 'Liveness & Doc Verification', status: 'ACTIVE', verifiedToday: 89, flaggedCount: 0, avgLatency: '2.4s' }]);const [identityLogStream, setIdentityLogStream] = useState([{ id: 'ID-9901', timestamp: '13:42:10', provider: 'Persona', subject: 'usr_inst_8829', result: 'PASS', score: '0.99' },{ id: 'ID-9902', timestamp: '13:44:05', provider: 'Veriff', subject: 'usr_inst_9102', result: 'FLAGGED_PEP', score: '0.45' },{ id: 'ID-9903', timestamp: '13:48:30', provider: 'Persona', subject: 'usr_inst_3341', result: 'PASS', score: '0.97' }]);// Funding & Brokerage Rails State (Plaid, Circle, Alpaca, Drivewealth)const [brokerageRails, setBrokerageRails] = useState([{ id: 'rail-alpaca', name: 'Alpaca Brokerage Clearing', assetClass: 'US Equities / Omnibus', status: 'ONLINE', rateLimit: '120 req/s', liquidityPool: '$14.2M' },{ id: 'rail-drivewealth', name: 'DriveWealth Fractional Execution', assetClass: 'Fractional Shares', status: 'ONLINE', rateLimit: '80 req/s', liquidityPool: '$8.5M' },{ id: 'rail-circle', name: 'Circle USDC Mint/Redeem', assetClass: 'Digital Asset Clearing', status: 'ONLINE', rateLimit: '50 req/s', liquidityPool: '$22.1M' },{ id: 'rail-plaid', name: 'Plaid ACH Institutional Banking', assetClass: 'Fiat Gateway / Same-Day ACH', status: 'ONLINE', rateLimit: '200 req/s', liquidityPool: '$45.0M' }]);// Cloudflare Status Atom Feed Monitor Stateconst [selectedIncident, setSelectedIncident] = useState({id: 'tag:cloudflarestatus.com,2014:Incident/kv-replication-delay',title: 'Workers KV Replication Sync Delay',published: '2026-08-30T02:05:00Z',updated: '2026-08-30T04:12:11Z',link: 'https://cloudflarestatus.com',status: 'Monitoring',content: 'KV cache invalidation sequences executing under limited velocity thresholds. Cache persistence operations safe.'});const cloudflareIncidentsFeed = [{id: 'tag:cloudflarestatus.com,2014:Incident/kv-replication-delay',title: 'Workers KV Replication Sync Delay',published: '2026-08-30T02:05:00Z',updated: '2026-08-30T04:12:11Z',link: 'https://cloudflarestatus.com',status: 'Monitoring',content: 'KV cache invalidation sequences executing under limited velocity thresholds. Cache persistence operations safe.',rawXml: <?xml version="1.0" encoding="UTF-8"?>\n<entry>\n  <id>tag:cloudflarestatus.com,2014:Incident/kv-replication-delay</id>\n  <published>2026-08-30T02:05:00Z</published>\n  <updated>2026-08-30T04:12:11Z</updated>\n  <link href="https://cloudflarestatus.com" rel="alternate"/>\n  <title>Workers KV Replication Sync Delay</title>\n  <content type="html">&lt;p&gt;&lt;strong&gt;Monitoring&lt;/strong&gt;: Cache invalidation sequence tracking velocity limit...&lt;/p&gt;</content>\n</entry>},{id: 'tag:cloudflarestatus.com,2014:Incident/edge-routing-772',title: 'Tier-1 BGP Route Leakage Change',published: '2026-08-29T14:10:00Z',updated: '2026-08-29T15:22:00Z',link: 'https://cloudflarestatus.com',status: 'Resolved',content: 'Autonomous system path definitions corrected. Ingress latency metrics across standard routes have normalized back to baseline.',rawXml: <?xml version="1.0" encoding="UTF-8"?>\n<entry>\n  <id>tag:cloudflarestatus.com,2014:Incident/edge-routing-772</id>\n  <published>2026-08-29T14:10:00Z</published>\n  <updated>2026-08-29T15:22:00Z</updated>\n  <link href="https://cloudflarestatus.com" rel="alternate"/>\n  <title>Tier-1 BGP Route Leakage Change</title>\n  <content type="html">&lt;p&gt;&lt;strong&gt;Resolved&lt;/strong&gt;: AS path definitions corrected...&lt;/p&gt;</content>\n</entry>},{id: 'tag:cloudflarestatus.com,2014:Incident/cp306tmzcl0y',title: 'Unplanned Database Outage',published: '2014-05-14T20:22:39Z',updated: '2014-05-14T20:35:21Z',link: 'https://cloudflarestatus.com',status: 'Identified',content: 'Our master database is down. Ingress traffic parameters are currently routed to read-only replica instances across distributed node layers while state restoration is processed.',rawXml: <?xml version="1.0" encoding="UTF-8"?>\n<entry>\n  <id>tag:cloudflarestatus.com,2014:Incident/cp306tmzcl0y</id>\n  <published>2014-05-14T20:22:39Z</published>\n  <updated>2014-05-14T20:35:21Z</updated>\n  <link href="https://cloudflarestatus.com" rel="alternate"/>\n  <title>Unplanned Database Outage</title>\n  <content type="html">&lt;p&gt;&lt;strong&gt;Identified&lt;/strong&gt;: Our master database is down...&lt;/p&gt;</content>\n</entry>}];// Sandbox Macro Hedging Contractsconst [macroHedgeContracts, setMacroHedgeContracts] = useState([{ id: 'pm-01', type: 'Central Bank Decision', title: 'Federal Reserve to lower target rate by ≥25bps in Q4', probability: 68, dynamicYield: '4.15%', poolVolume: '$4.2M', tradeState: 'OPEN' },{ id: 'pm-02', type: 'Inflation & Economic Data', title: 'Core CPI YoY remains above 2.8% in next printing', probability: 42, dynamicYield: '5.20%', poolVolume: '$2.8M', tradeState: 'OPEN' },{ id: 'pm-03', type: 'Energy & Commodity Trends', title: 'Brent Crude breaches $88/bbl by end of September', probability: 55, dynamicYield: '6.85%', poolVolume: '$6.1M', tradeState: 'OPEN' },{ id: 'pm-04', type: 'Geopolitical Developments', title: 'EU trade framework renegotiation successfully signed', probability: 19, dynamicYield: '2.10%', poolVolume: '$1.9M', tradeState: 'SUSPENDED' }]);// Governance Multi-Signatory Stateconst [governancePolicies, setGovernancePolicies] = useState([{ id: 'gov-101', title: 'Break-Glass Protocol Root Trigger', signatureSchema: 'M-of-N Cryptographic', signaturesReceived: 1, signaturesRequired: 3, signatories: ['SEC_OPS_01'], status: 'LOCKED' },{ id: 'gov-102', title: 'Stripe Webhook HMAC Key Rotation', signatureSchema: 'Dual-Custody Mandate', signaturesReceived: 1, signaturesRequired: 2, signatories: ['FIN_CORE_02'], status: 'PENDING' },{ id: 'gov-103', title: 'Alpaca Omnibus Clearing Parameter Shift', signatureSchema: 'Multi-Party Consent', signaturesReceived: 2, signaturesRequired: 2, signatories: ['BROKER_OPS_01', 'COMPLIANCE_DIR_04'], status: 'EXECUTED' }]);// Telemetry Metrics Stateconst [metrics, setMetrics] = useState({cpuUsage: 42.4,memoryUsage: 68.1,networkThroughput: 1.25,activeConnections: 1420});// Hardened Tier-0 Admin Console Stateconst [circuitBreakerActive, setCircuitBreakerActive] = useState(false);const [webAuthnPending, setWebAuthnPending] = useState(false);const [pendingAdminAction, setPendingAdminAction] = useState(null);const [quorumRequests, setQuorumRequests] = useState([{ id: 'REQ-8801', action: 'GLOBAL_CIRCUIT_BREAKER_ENGAGE', maker: 'secops-maker@apexcapital.internal', timestamp: '2026-08-30 13:48:10', status: 'PENDING_CHECKER_APPROVAL', source: 'sandbox-mock' }]);const [unredactedLogs, setUnredactedLogs] = useState([{ id: 'LOG-001', timestamp: '2026-08-30 13:40:12', actor: 'secops-lead@apexcapital.internal', sourceIp: '10.0.4.15', action: 'SALESFORCE_TOKEN_FLUSH', detail: 'OAuth grant invalidation triggered via proxy gateway assertion.', source: 'sandbox-mock', sha256: 'e3b0c44288fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855' },{ id: 'LOG-002', timestamp: '2026-08-30 13:42:05', actor: 'HSM_CORE_NODE_01', sourceIp: '127.0.0.1', action: 'QUORUM_KEY_ROTATION', detail: 'Master Ed25519 seed key rotated under dual-control policy attestation.', source: 'sandbox-mock', sha256: 'a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e' }]);// Live Metrics Simulator HookuseEffect(() => {if (!isLiveStream) return;const interval = setInterval(() => {setMetrics(prev => ({cpuUsage: +(Math.min(95, Math.max(15, prev.cpuUsage + (Math.random() * 4 - 2))).toFixed(1)),memoryUsage: +(Math.min(90, Math.max(40, prev.memoryUsage + (Math.random() * 2 - 1))).toFixed(1)),networkThroughput: +(Math.max(0.5, prev.networkThroughput + (Math.random() * 0.2 - 0.1)).toFixed(2)),activeConnections: Math.floor(Math.max(800, prev.activeConnections + (Math.random() * 20 - 10)))}));}, 2000);return () => clearInterval(interval);}, [isLiveStream]);const triggerToast = (msg) => {setNotification(msg);setTimeout(() => setNotification(null), 4000);};const triggerAdminApproval = () => {setIsAdminApproved(true);setSalesforceLogs(prev => [{ timestamp: new Date().toTimeString().split(' ')[0], type: 'WARN', message: 'SEC_OPS authority bypass signature injected. Step 1 cleared.' },...prev]);triggerToast("Cryptographic SEC_OPS override signature applied.");};const handleMfaSubmit = (e) => {e.preventDefault();if (mfaInputCode.trim() === '654321' || mfaInputCode.trim() === '882019') {setIsMfaVerified(true);setSalesforceConnectorStatus('CONNECTED');setMfaError('');setSalesforceLogs(prev => [{ timestamp: new Date().toTimeString().split(' ')[0], type: 'INFO', message: 'MFA attestation verified successfully. Tunnel ACTIVE.' },...prev]);triggerToast('Salesforce OAuth Connector tunnel established successfully.');} else {setMfaError('Invalid MFA token. Enter "654321" or "882019" for mock pass.');}};const executeHedgeSimulation = (id, direction) => {setMacroHedgeContracts(prev => prev.map(contract => {if (contract.id === id) {const delta = direction === 'UP' ? 4 : -4;const targetProb = Math.min(Math.max(contract.probability + delta, 1), 99);return { ...contract, probability: targetProb };}return contract;}));triggerToast('Adjusted target contract parameter weight.');};const castGovernanceSignature = (id) => {setGovernancePolicies(prev => prev.map(policy => {if (policy.id === id && policy.signaturesReceived < policy.signaturesRequired) {const updatedCount = policy.signaturesReceived + 1;const currentSignatories = [...policy.signatories, AUTH_NODE_0${updatedCount}];return {...policy,signaturesReceived: updatedCount,signatories: currentSignatories,status: updatedCount === policy.signaturesRequired ? 'EXECUTED' : 'PENDING'};}return policy;}));triggerToast('Injected cryptographic validation signature into quorum ledger.');};const initiateAdminStepUp = (actionType, payload = {}) => {setPendingAdminAction({ actionType, payload });setWebAuthnPending(true);};const handleWebAuthnVerify = () => {setWebAuthnPending(false);if (pendingAdminAction?.actionType === 'TOGGLE_CIRCUIT_BREAKER') {const nextState = !circuitBreakerActive;setCircuitBreakerActive(nextState);const newLog = {id: LOG-00${unredactedLogs.length + 1},timestamp: new Date().toISOString().replace('T', ' ').substring(0, 19),actor: 'secops-lead@apexcapital.internal',sourceIp: '10.0.4.15',action: nextState ? 'CIRCUIT_BREAKER_ENGAGED' : 'CIRCUIT_BREAKER_DISENGAGED',detail: nextState ? 'Global emergency halt applied via WebAuthn step-up.' : 'Normal operation restored.',source: 'sandbox-mock',sha256: '8f434346648f6b96df89dda901c5176b10a6d83961dd3c1ac88b59b2dc327aa4'};setUnredactedLogs(prev => [newLog, ...prev]);triggerToast(nextState ? 'Circuit Breaker ENGAGED.' : 'Circuit Breaker DISENGAGED.');} else if (pendingAdminAction?.actionType === 'APPROVE_QUORUM') {setQuorumRequests(prev => prev.filter(r => r.id !== pendingAdminAction.payload.reqId));triggerToast('Quorum Checker Approval recorded.');}setPendingAdminAction(null);};// UI styling class definitionsconst classes = {layout: 'min-h-screen bg-slate-950 text-slate-100 flex flex-col font-sans antialiased selection:bg-indigo-500/30',header: 'border-b border-slate-800 bg-slate-900/60 backdrop-blur-xl px-6 py-4 flex flex-col md:flex-row items-center justify-between gap-4 sticky top-0 z-40',mainLayout: 'flex-1 flex flex-col md:flex-row overflow-hidden',nav: 'w-full md:w-64 bg-slate-900/40 backdrop-blur-md border-b md:border-b-0 md:border-r border-slate-800/80 p-5 flex flex-col justify-between gap-6 flex-shrink-0',navButton: 'w-full flex items-center justify-between px-3 py-2.5 rounded-xl text-xs font-medium transition-all duration-200 outline-none',navButtonActive: 'bg-indigo-600 text-white shadow-lg shadow-indigo-600/20',navButtonInactive: 'text-slate-400 hover:bg-slate-800/60 hover:text-slate-200',main: 'flex-1 bg-slate-950 p-6 overflow-y-auto flex flex-col gap-6 w-full max-w-[1600px] mx-auto',card: 'bg-slate-900 border border-slate-800 rounded-2xl p-5 shadow-xl transition-all duration-200',buttonPrimary: 'bg-indigo-600 hover:bg-indigo-500 text-white font-mono text-xs px-4 py-2 rounded-xl font-bold tracking-wide transition-all shadow-md active:scale-95 flex items-center gap-1.5',buttonSecondary: 'bg-slate-900 hover:bg-slate-800 text-slate-300 font-mono text-xs px-3.5 py-1.5 rounded-xl border border-slate-700 transition-all flex items-center gap-2',inputField: 'bg-slate-950 text-slate-100 font-mono text-xs border border-slate-700 rounded-lg px-3 py-1.5 focus:outline-none focus:border-indigo-500 placeholder:text-slate-600 transition-colors',footer: 'bg-slate-900 border-t border-slate-800 px-6 py-2.5 text-[11px] flex flex-col sm:flex-row justify-between items-center gap-2 mt-auto w-full'};return ({/* Toast Banner */}{notification && ({notification}<button onClick={() => setNotification(null)} className="text-white hover:text-slate-200 font-bold text-sm">×)}  {/* Header */}
  <header className={classes.header}>
    <div className="flex items-center gap-3">
      <div className="p-2.5 bg-indigo-600/20 text-indigo-400 rounded-xl border border-indigo-500/30 shadow-inner">
        <Layers size={22} className="animate-pulse" />
      </div>
      <div>
        <h1 className="text-sm font-semibold tracking-wider text-slate-100 uppercase flex items-center gap-2">
          Apex Enterprise Control Plane
          <span className="text-[10px] bg-slate-800 font-mono tracking-normal normal-case text-slate-400 px-2 py-0.5 rounded">v2.1.0-Prod</span>
        </h1>
        <p className="text-xs text-slate-400 font-mono">Edge Routing • Identity Ingress • Multi-Party Settlement</p>
      </div>
    </div>

    {/* Global Live Stream Control & Header Indicators */}
    <div className="flex items-center gap-4">
      <div className="flex items-center gap-2 bg-slate-950 border border-slate-800 px-3 py-1.5 rounded-xl font-mono text-xs">
        <span className={`w-2 h-2 rounded-full ${isLiveStream ? 'bg-emerald-400 animate-ping' : 'bg-amber-400'}`} />
        <span className="text-slate-300">{isLiveStream ? 'STREAM ACTIVE' : 'STREAM PAUSED'}</span>
        <button 
          onClick={() => setIsLiveStream(!isLiveStream)}
          className="ml-2 text-slate-400 hover:text-slate-100 transition-colors"
        >
          <RefreshCw size={12} className={isLiveStream ? 'animate-spin' : ''} />
        </button>
      </div>
    </div>
  </header>

  {/* Main Workspace */}
  <div className={classes.mainLayout}>
    {/* Navigation Sidebar */}
    <nav className={classes.nav}>
      <div className="flex flex-col gap-1.5">
        <span className="text-[10px] font-mono font-bold uppercase tracking-wider text-slate-500 px-3 mb-1">Operational Modules</span>
        
        <button 
          onClick={() => setActiveTab('cloudflare')}
          className={`${classes.navButton} ${activeTab === 'cloudflare' ? classes.navButtonActive : classes.navButtonInactive}`}
        >
          <span className="flex items-center gap-2.5"><Rss size={16} /> Cloudflare Status Feed</span>
          <span className="text-[10px] font-mono bg-slate-950/40 px-1.5 py-0.5 rounded">Atom</span>
        </button>

        <button 
          onClick={() => setActiveTab('salesforce')}
          className={`${classes.navButton} ${activeTab === 'salesforce' ? classes.navButtonActive : classes.navButtonInactive}`}
        >
          <span className="flex items-center gap-2.5"><Key size={16} /> Salesforce OAuth Connector</span>
          <span className={`text-[10px] font-mono px-1.5 py-0.5 rounded ${isMfaVerified ? 'bg-emerald-950 text-emerald-400' : 'bg-rose-950 text-rose-400'}`}>
            {isMfaVerified ? 'OK' : 'ERR'}
          </span>
        </button>

        <button 
          onClick={() => setActiveTab('identity')}
          className={`${classes.navButton} ${activeTab === 'identity' ? classes.navButtonActive : classes.navButtonInactive}`}
        >
          <span className="flex items-center gap-2.5"><BadgeCheck size={16} /> Identity & KYC (Persona)</span>
          <span className="text-[10px] font-mono bg-emerald-950 text-emerald-400 px-1.5 py-0.5 rounded">2 Active</span>
        </button>

        <button 
          onClick={() => setActiveTab('brokerage')}
          className={`${classes.navButton} ${activeTab === 'brokerage' ? classes.navButtonActive : classes.navButtonInactive}`}
        >
          <span className="flex items-center gap-2.5"><Briefcase size={16} /> Clearing Rails (Alpaca/Plaid)</span>
          <span className="text-[10px] font-mono bg-slate-950/40 px-1.5 py-0.5 rounded">4 Rails</span>
        </button>

        <button 
          onClick={() => setActiveTab('macro')}
          className={`${classes.navButton} ${activeTab === 'macro' ? classes.navButtonActive : classes.navButtonInactive}`}
        >
          <span className="flex items-center gap-2.5"><TrendingUp size={16} /> Macro Hedging Sandbox</span>
          <span className="text-[10px] font-mono bg-slate-950/40 px-1.5 py-0.5 rounded">{macroHedgeContracts.length}</span>
        </button>

        <button 
          onClick={() => setActiveTab('governance')}
          className={`${classes.navButton} ${activeTab === 'governance' ? classes.navButtonActive : classes.navButtonInactive}`}
        >
          <span className="flex items-center gap-2.5"><Scale size={16} /> Governance Quorum</span>
          <span className="text-[10px] font-mono bg-slate-950/40 px-1.5 py-0.5 rounded">M-of-N</span>
        </button>

        <button 
          onClick={() => setActiveTab('telemetry')}
          className={`${classes.navButton} ${activeTab === 'telemetry' ? classes.navButtonActive : classes.navButtonInactive}`}
        >
          <span className="flex items-center gap-2.5"><Cpu size={16} /> Edge Telemetry Metrics</span>
          <span className="text-[10px] font-mono bg-emerald-950 text-emerald-400 px-1.5 py-0.5 rounded">Live</span>
        </button>

        <span className="text-[10px] font-mono font-bold uppercase tracking-wider text-rose-500/80 px-3 mt-4 mb-1">Tier-0 Admin Surface</span>
        <button 
          onClick={() => setActiveTab('admin')}
          className={`${classes.navButton} ${activeTab === 'admin' ? 'bg-rose-600 text-white shadow-lg shadow-rose-600/20' : 'text-rose-400 hover:bg-rose-950/30'}`}
        >
          <span className="flex items-center gap-2.5"><ShieldAlert size={16} /> Master Admin Console</span>
          <span className="text-[9px] font-mono bg-rose-950 text-rose-300 px-1.5 py-0.5 rounded border border-rose-800">Root</span>
        </button>
      </div>

      <div className="bg-slate-950/60 p-3 rounded-xl border border-slate-800/60 text-xs font-mono text-slate-400 flex flex-col gap-1">
        <div className="flex justify-between">
          <span>Origin Node:</span>
          <span className="text-slate-200">us-east-1</span>
        </div>
        <div className="flex justify-between">
          <span>Environment:</span>
          <span className="text-emerald-400">Production</span>
        </div>
      </div>
    </nav>

    {/* Main Workspace Body */}
    <main className={classes.main}>
      
      {/* TAB 1: CLOUDFLARE STATUS ATOM FEED */}
      {activeTab === 'cloudflare' && (
        <div className="flex flex-col gap-6">
          <div className="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 bg-slate-900 p-5 rounded-2xl border border-slate-800">
            <div>
              <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                <Rss size={18} className="text-indigo-400" /> Cloudflare Status Atom Incident Monitor
              </h2>
              <p className="text-xs text-slate-400 font-mono mt-0.5">Real-time RSS/Atom feed parsing with XML structure inspector.</p>
            </div>
            <button 
              onClick={() => setViewXmlMode(!viewXmlMode)}
              className={classes.buttonSecondary}
            >
              <Code size={14} /> {viewXmlMode ? 'Switch to Formatted Entry' : 'View Raw Atom XML'}
            </button>
          </div>

          <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
            {/* Incident Stream */}
            <div className="flex flex-col gap-3">
              <span className="text-xs font-mono text-slate-400 font-bold uppercase tracking-wider">Feed Stream Entries</span>
              {cloudflareIncidentsFeed.map(incident => (
                <div 
                  key={incident.id} 
                  onClick={() => setSelectedIncident(incident)}
                  className={`p-4 rounded-xl border cursor-pointer transition-all ${
                    selectedIncident.id === incident.id 
                      ? 'bg-indigo-950/40 border-indigo-500/50 shadow-lg' 
                      : 'bg-slate-900 border-slate-800 hover:border-slate-700'
                  }`}
                >
                  <div className="flex items-center justify-between mb-1.5">
                    <span className={`text-[10px] font-mono px-2 py-0.5 rounded uppercase font-bold ${
                      incident.status === 'Resolved' ? 'bg-emerald-950 text-emerald-400 border border-emerald-800' :
                      incident.status === 'Monitoring' ? 'bg-amber-950 text-amber-400 border border-amber-800' :
                      'bg-rose-950 text-rose-400 border border-rose-800'
                    }`}>
                      {incident.status}
                    </span>
                    <span className="text-[10px] font-mono text-slate-500">{incident.published.substring(0, 10)}</span>
                  </div>
                  <h3 className="text-xs font-bold text-slate-200">{incident.title}</h3>
                </div>
              ))}
            </div>

            {/* Selected Entry Detail Viewer */}
            <div className="lg:col-span-2 bg-slate-900 border border-slate-800 rounded-2xl p-6 flex flex-col gap-4">
              <div className="border-b border-slate-800 pb-4">
                <span className="text-[10px] font-mono text-indigo-400 uppercase font-bold tracking-wider">Active Selection Detail</span>
                <h2 className="text-base font-bold text-slate-100 mt-1">{selectedIncident.title}</h2>
                <span className="text-xs font-mono text-slate-500">{selectedIncident.id}</span>
              </div>

              {!viewXmlMode ? (
                <div className="flex flex-col gap-4 font-mono text-xs">
                  <div className="bg-slate-950 p-4 rounded-xl border border-slate-850 text-slate-300 leading-relaxed">
                    {selectedIncident.content}
                  </div>
                  <div className="grid grid-cols-2 gap-4">
                    <div className="bg-slate-950 p-3 rounded-lg border border-slate-850">
                      <span className="text-[10px] text-slate-500 block">PUBLISHED</span>
                      <span className="text-slate-200">{selectedIncident.published}</span>
                    </div>
                    <div className="bg-slate-950 p-3 rounded-lg border border-slate-850">
                      <span className="text-[10px] text-slate-500 block">UPDATED</span>
                      <span className="text-slate-200">{selectedIncident.updated}</span>
                    </div>
                  </div>
                </div>
              ) : (
                <pre className="bg-slate-950 p-4 rounded-xl border border-slate-800 font-mono text-[11px] text-indigo-300 overflow-x-auto whitespace-pre-wrap leading-relaxed">
                  {selectedIncident.rawXml || '<?xml version="1.0" encoding="UTF-8"?>\n<entry>\n  <id>' + selectedIncident.id + '</id>\n</entry>'}
                </pre>
              )}
            </div>
          </div>
        </div>
      )}

      {/* TAB 2: SALESFORCE CONNECTOR */}
      {activeTab === 'salesforce' && (
        <div className="flex flex-col gap-6 max-w-4xl mx-auto w-full">
          <div className="bg-slate-900 p-6 rounded-2xl border border-slate-800 flex flex-col gap-6">
            <div className="flex items-center justify-between border-b border-slate-800 pb-4">
              <div>
                <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                  <Key size={18} className="text-amber-400" /> Salesforce Admin Connector Diagnostic
                </h2>
                <p className="text-xs text-slate-400 font-mono mt-0.5">OAuth handshake verification and step-up MFA authorization.</p>
              </div>
              <span className={`text-xs font-mono font-bold px-3 py-1 rounded-xl border ${
                isMfaVerified ? 'bg-emerald-950 text-emerald-400 border-emerald-800' : 'bg-rose-950 text-rose-400 border-rose-800'
              }`}>
                STATUS: {salesforceConnectorStatus}
              </span>
            </div>

            {/* Step 1 & Step 2 Sequential Resolution Panel */}
            <div className="flex flex-col gap-4">
              {/* Step 1: Override */}
              <div className={`p-4 rounded-xl border flex flex-col gap-2 transition-all ${
                isAdminApproved ? 'bg-slate-950/40 border-slate-800 text-slate-400' : 'bg-slate-950 border-amber-500/30'
              }`}>
                <div className="flex justify-between items-center">
                  <span className="text-xs font-mono font-bold text-slate-200 flex items-center gap-2">
                    <span className="w-5 h-5 rounded-full bg-amber-500 text-slate-950 flex items-center justify-center text-[10px] font-bold">1</span>
                    Inject Cryptographic SEC_OPS Authority Bypass Signature
                  </span>
                  {isAdminApproved ? (
                    <span className="text-xs font-mono text-emerald-400 font-bold flex items-center gap-1"><CheckCircle2 size={14} /> SIGNED</span>
                  ) : (
                    <button onClick={triggerAdminApproval} className={classes.buttonPrimary}>
                      Sign Exception Override
                    </button>
                  )}
                </div>
              </div>

              {/* Step 2: MFA Input */}
              <div className={`p-4 rounded-xl border flex flex-col gap-3 transition-all ${
                !isAdminApproved ? 'opacity-50 pointer-events-none bg-slate-950 border-slate-800' : 
                isMfaVerified ? 'bg-slate-950/40 border-slate-800' : 'bg-slate-950 border-indigo-500/30'
              }`}>
                <div className="flex justify-between items-center">
                  <span className="text-xs font-mono font-bold text-slate-200 flex items-center gap-2">
                    <span className="w-5 h-5 rounded-full bg-indigo-600 text-white flex items-center justify-center text-[10px] font-bold">2</span>
                    Submit Hardware MFA Token Injection
                  </span>
                  {isMfaVerified && <span className="text-xs font-mono text-emerald-400 font-bold flex items-center gap-1"><CheckCircle2 size={14} /> VERIFIED</span>}
                </div>

                {!isMfaVerified && isAdminApproved && (
                  <form onSubmit={handleMfaSubmit} className="flex flex-col gap-3 mt-1">
                    <div className="flex gap-2">
                      <input 
                        type="text" 
                        placeholder="Input Code: 654321" 
                        value={mfaInputCode}
                        onChange={(e) => setMfaInputCode(e.target.value)}
                        className={classes.inputField + ' flex-1'}
                      />
                      <button type="submit" className={classes.buttonPrimary}>
                        Verify MFA & Re-Establish
                      </button>
                    </div>
                    {mfaError && <span className="text-xs text-rose-400 font-mono">{mfaError}</span>}
                  </form>
                )}
              </div>
            </div>

            {/* Live Terminal Log Output */}
            <div className="bg-slate-950 border border-slate-800 rounded-xl overflow-hidden">
              <div className="bg-slate-900 px-4 py-2 border-b border-slate-800 text-[10px] font-mono text-slate-400 uppercase flex items-center justify-between">
                <span>Connector Log Stream</span>
                <Terminal size={12} />
              </div>
              <div className="p-4 font-mono text-[11px] flex flex-col gap-1.5">
                {salesforceLogs.map((log, idx) => (
                  <div key={idx} className="flex items-center gap-2">
                    <span className="text-slate-500">[{log.timestamp}]</span>
                    <span className={log.type === 'ERROR' ? 'text-rose-400 font-bold' : log.type === 'WARN' ? 'text-amber-400' : 'text-emerald-400'}>
                      [{log.type}]
                    </span>
                    <span className="text-slate-300">{log.message}</span>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      )}

      {/* TAB 3: IDENTITY & KYC (PERSONA / VERIFF) */}
      {activeTab === 'identity' && (
        <div className="flex flex-col gap-6">
          <div className="bg-slate-900 p-5 rounded-2xl border border-slate-800 flex justify-between items-center">
            <div>
              <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                <BadgeCheck size={18} className="text-emerald-400" /> Identity Verification & Institutional KYC (Persona / Veriff)
              </h2>
              <p className="text-xs text-slate-400 font-mono mt-0.5">Biometric liveness, PEP/sanctions screening, and compliance verification webhooks.</p>
            </div>
            <button 
              onClick={() => triggerToast("Injected simulated Persona verification webhook.")}
              className={classes.buttonSecondary}
            >
              <RefreshCw size={12} /> Trigger Test Inquiry
            </button>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
            {identityProviders.map(provider => (
              <div key={provider.id} className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col justify-between gap-4">
                <div className="flex items-center justify-between">
                  <span className="text-xs font-mono font-bold text-slate-200">{provider.name}</span>
                  <span className="text-[10px] font-mono bg-emerald-950 text-emerald-400 px-2 py-0.5 rounded border border-emerald-800 font-bold">
                    {provider.status}
                  </span>
                </div>

                <div className="grid grid-cols-3 gap-2 bg-slate-950 p-3 rounded-xl border border-slate-850 font-mono text-xs">
                  <div>
                    <span className="text-[9px] text-slate-500 block">VERIFIED (24H)</span>
                    <span className="text-emerald-400 font-bold">{provider.verifiedToday}</span>
                  </div>
                  <div>
                    <span className="text-[9px] text-slate-500 block">FLAGGED</span>
                    <span className="text-rose-400 font-bold">{provider.flaggedCount}</span>
                  </div>
                  <div>
                    <span className="text-[9px] text-slate-500 block">AVG LATENCY</span>
                    <span className="text-slate-300">{provider.avgLatency}</span>
                  </div>
                </div>
              </div>
            ))}
          </div>

          {/* Ingress Stream */}
          <div className="bg-slate-900 border border-slate-800 rounded-2xl p-5 flex flex-col gap-3">
            <span className="text-xs font-mono font-bold uppercase text-slate-400">Live Ingress Verification Stream</span>
            <div className="flex flex-col gap-2 font-mono text-xs">
              {identityLogStream.map(log => (
                <div key={log.id} className="bg-slate-950 p-3 rounded-xl border border-slate-850 flex items-center justify-between">
                  <div className="flex items-center gap-3">
                    <span className="text-slate-500">{log.timestamp}</span>
                    <span className="text-indigo-400 font-bold">{log.provider}</span>
                    <span className="text-slate-300">{log.subject}</span>
                  </div>
                  <div className="flex items-center gap-3">
                    <span className="text-slate-500">Score: {log.score}</span>
                    <span className={`px-2 py-0.5 rounded text-[10px] font-bold ${
                      log.result === 'PASS' ? 'bg-emerald-950 text-emerald-400 border border-emerald-800' : 'bg-rose-950 text-rose-400 border border-rose-800'
                    }`}>
                      {log.result}
                    </span>
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      )}

      {/* TAB 4: CLEARING RAILS (ALPACA / DRIVEWEALTH / CIRCLE / PLAID) */}
      {activeTab === 'brokerage' && (
        <div className="flex flex-col gap-6">
          <div className="bg-slate-900 p-5 rounded-2xl border border-slate-800 flex justify-between items-center">
            <div>
              <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                <Briefcase size={18} className="text-indigo-400" /> Institutional Clearing & Brokerage Execution Gateway
              </h2>
              <p className="text-xs text-slate-400 font-mono mt-0.5">Alpaca Equity Clearing, DriveWealth Fractional Execution, Circle USDC, and Plaid ACH.</p>
            </div>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
            {brokerageRails.map(rail => (
              <div key={rail.id} className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col gap-4">
                <div className="flex items-center justify-between">
                  <span className="text-xs font-mono font-bold text-slate-200">{rail.name}</span>
                  <span className="text-[10px] font-mono bg-emerald-950 text-emerald-400 px-2 py-0.5 rounded border border-emerald-800 font-bold">
                    {rail.status}
                  </span>
                </div>

                <p className="text-xs text-slate-400 font-mono">{rail.assetClass}</p>

                <div className="grid grid-cols-2 gap-2 bg-slate-950 p-3 rounded-xl border border-slate-850 font-mono text-xs">
                  <div>
                    <span className="text-[9px] text-slate-500 block">THROUGHPUT CAPACITY</span>
                    <span className="text-indigo-300 font-bold">{rail.rateLimit}</span>
                  </div>
                  <div>
                    <span className="text-[9px] text-slate-500 block">LIQUIDITY BUFFER</span>
                    <span className="text-emerald-400 font-bold">{rail.liquidityPool}</span>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}

      {/* TAB 5: MACRO HEDGING SANDBOX */}
      {activeTab === 'macro' && (
        <div className="flex flex-col gap-6">
          <div className="bg-slate-900 p-5 rounded-2xl border border-slate-800 flex justify-between items-center">
            <div>
              <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                <TrendingUp size={18} className="text-indigo-400" /> Macro Hedging Sandbox Event Contracts
              </h2>
              <p className="text-xs text-slate-400 font-mono mt-0.5">Adjust target contract weights to simulate dynamic yield curve rebalancing.</p>
            </div>
            <span className="text-[10px] font-mono bg-indigo-950 text-indigo-300 px-2.5 py-1 rounded border border-indigo-800">
              SANDBOX-MOCK
            </span>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
            {macroHedgeContracts.map(contract => (
              <div key={contract.id} className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col justify-between gap-4">
                <div className="flex items-center justify-between">
                  <span className="text-[10px] font-mono text-indigo-400 bg-indigo-950 px-2 py-0.5 rounded border border-indigo-800">
                    {contract.type}
                  </span>
                  <span className={`text-[10px] font-mono px-2 py-0.5 rounded font-bold ${
                    contract.tradeState === 'OPEN' ? 'bg-emerald-950 text-emerald-400' : 'bg-rose-950 text-rose-400'
                  }`}>
                    {contract.tradeState}
                  </span>
                </div>

                <h3 className="text-xs font-bold text-slate-100 leading-snug">{contract.title}</h3>

                <div className="grid grid-cols-3 gap-2 bg-slate-950 p-3 rounded-xl border border-slate-850 font-mono text-xs">
                  <div>
                    <span className="text-[9px] text-slate-500 block">PROBABILITY</span>
                    <span className="text-indigo-300 font-bold">{contract.probability}%</span>
                  </div>
                  <div>
                    <span className="text-[9px] text-slate-500 block">DYNAMIC YIELD</span>
                    <span className="text-emerald-400 font-bold">{contract.dynamicYield}</span>
                  </div>
                  <div>
                    <span className="text-[9px] text-slate-500 block">POOL VOLUME</span>
                    <span className="text-slate-300">{contract.poolVolume}</span>
                  </div>
                </div>

                <div className="flex gap-2">
                  <button 
                    onClick={() => executeHedgeSimulation(contract.id, 'UP')}
                    className="flex-1 bg-slate-800 hover:bg-slate-700 text-slate-200 font-mono text-xs py-1.5 rounded-lg border border-slate-700 flex items-center justify-center gap-1"
                  >
                    <ArrowUpRight size={14} className="text-emerald-400" /> Increase Weight
                  </button>
                  <button 
                    onClick={() => executeHedgeSimulation(contract.id, 'DOWN')}
                    className="flex-1 bg-slate-800 hover:bg-slate-700 text-slate-200 font-mono text-xs py-1.5 rounded-lg border border-slate-700 flex items-center justify-center gap-1"
                  >
                    <ArrowDownRight size={14} className="text-rose-400" /> Decrease Weight
                  </button>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}

      {/* TAB 6: GOVERNANCE QUORUM */}
      {activeTab === 'governance' && (
        <div className="flex flex-col gap-6">
          <div className="bg-slate-900 p-5 rounded-2xl border border-slate-800 flex justify-between items-center">
            <div>
              <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                <Scale size={18} className="text-indigo-400" /> Multi-Party Governance Quorum Ledger
              </h2>
              <p className="text-xs text-slate-400 font-mono mt-0.5">Cryptographic signature thresholds required for critical parameter execution.</p>
            </div>
          </div>

          <div className="flex flex-col gap-4">
            {governancePolicies.map(policy => (
              <div key={policy.id} className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col md:flex-row items-start md:items-center justify-between gap-4">
                <div className="flex flex-col gap-1">
                  <div className="flex items-center gap-2">
                    <span className="text-xs font-mono font-bold text-indigo-400">{policy.id}</span>
                    <h3 className="text-xs font-bold text-slate-100">{policy.title}</h3>
                  </div>
                  <span className="text-[10px] font-mono text-slate-400">Schema: {policy.signatureSchema}</span>
                </div>

                <div className="flex items-center gap-4 w-full md:w-auto justify-between md:justify-end">
                  <div className="font-mono text-xs text-right">
                    <span className="text-slate-400 block text-[10px]">SIGNATURES</span>
                    <span className="text-slate-200 font-bold">{policy.signaturesReceived} / {policy.signaturesRequired}</span>
                  </div>

                  <button 
                    disabled={policy.signaturesReceived >= policy.signaturesRequired}
                    onClick={() => castGovernanceSignature(policy.id)}
                    className={`${classes.buttonPrimary} disabled:opacity-50 disabled:cursor-not-allowed`}
                  >
                    <Key size={12} /> Inject Signature
                  </button>
                </div>
              </div>
            ))}
          </div>
        </div>
      )}

      {/* TAB 7: TELEMETRY METRICS */}
      {activeTab === 'telemetry' && (
        <div className="flex flex-col gap-6">
          <div className="bg-slate-900 p-5 rounded-2xl border border-slate-800 flex justify-between items-center">
            <div>
              <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                <Cpu size={18} className="text-emerald-400" /> Real-time Edge Node Infrastructure Telemetry
              </h2>
              <p className="text-xs text-slate-400 font-mono mt-0.5">Live CPU, memory, throughput, and active socket streaming.</p>
            </div>
          </div>

          <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
            <div className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col gap-1">
              <span className="text-[10px] font-mono text-slate-500 font-bold uppercase">CPU Core Load</span>
              <span className="text-2xl font-mono font-bold text-indigo-400">{metrics.cpuUsage}%</span>
              <div className="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden mt-2">
                <div className="bg-indigo-500 h-full transition-all duration-500" style={{ width: `${metrics.cpuUsage}%` }} />
              </div>
            </div>

            <div className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col gap-1">
              <span className="text-[10px] font-mono text-slate-500 font-bold uppercase">Memory Consumption</span>
              <span className="text-2xl font-mono font-bold text-amber-400">{metrics.memoryUsage}%</span>
              <div className="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden mt-2">
                <div className="bg-amber-500 h-full transition-all duration-500" style={{ width: `${metrics.memoryUsage}%` }} />
              </div>
            </div>

            <div className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col gap-1">
              <span className="text-[10px] font-mono text-slate-500 font-bold uppercase">Network Throughput</span>
              <span className="text-2xl font-mono font-bold text-emerald-400">{metrics.networkThroughput} Gbps</span>
              <div className="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden mt-2">
                <div className="bg-emerald-500 h-full transition-all duration-500" style={{ width: `${(metrics.networkThroughput / 2.5) * 100}%` }} />
              </div>
            </div>

            <div className="bg-slate-900 border border-slate-800 p-5 rounded-2xl flex flex-col gap-1">
              <span className="text-[10px] font-mono text-slate-500 font-bold uppercase">Active Connections</span>
              <span className="text-2xl font-mono font-bold text-slate-100">{metrics.activeConnections}</span>
              <div className="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden mt-2">
                <div className="bg-slate-400 h-full transition-all duration-500" style={{ width: `${(metrics.activeConnections / 2000) * 100}%` }} />
              </div>
            </div>
          </div>
        </div>
      )}

      {/* TAB 8: HARDENED TIER-0 MASTER ADMIN CONSOLE */}
      {activeTab === 'admin' && (
        <div className="flex flex-col gap-6">
          <div className="bg-slate-900 border border-rose-900/40 p-5 rounded-2xl flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
            <div className="flex items-center gap-3">
              <div className="p-2.5 bg-rose-600/20 text-rose-400 rounded-xl border border-rose-500/30">
                <ShieldAlert size={22} />
              </div>
              <div>
                <h2 className="text-sm font-bold uppercase tracking-wider text-slate-100 flex items-center gap-2">
                  Master Admin Control Console
                  <span className="text-[10px] bg-rose-950 text-rose-400 font-mono px-2 py-0.5 rounded border border-rose-800 font-bold">HARDENED TIER-0</span>
                </h2>
                <p className="text-xs text-slate-400 font-mono">Cloudflare Access Identity Verified • WebAuthn Step-Up Protection</p>
              </div>
            </div>

            <button 
              onClick={() => initiateAdminStepUp('TOGGLE_CIRCUIT_BREAKER')}
              className={`px-4 py-2 rounded-xl text-xs font-mono font-bold border transition-all flex items-center gap-2 ${
                circuitBreakerActive 
                  ? 'bg-rose-600 text-white border-rose-500 animate-pulse shadow-lg shadow-rose-600/30' 
                  : 'bg-slate-950 text-rose-400 border-rose-500/30 hover:bg-rose-950/40'
              }`}
            >
              <Zap size={14} />
              {circuitBreakerActive ? 'CIRCUIT BREAKER: ENGAGED' : 'ENGAGE CIRCUIT BREAKER'}
            </button>
          </div>

          {/* Hardware Key Modal */}
          {webAuthnPending && (
            <div className="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 flex items-center justify-center p-4">
              <div className="bg-slate-900 border border-slate-800 rounded-2xl p-6 max-w-md w-full flex flex-col gap-5 shadow-2xl">
                <div className="flex items-center gap-3">
                  <div className="p-3 bg-indigo-500/10 text-indigo-400 rounded-xl border border-indigo-500/20">
                    <Key size={24} />
                  </div>
                  <div>
                    <h3 className="text-sm font-bold text-slate-100 uppercase">Hardware Key Step-Up Required</h3>
                    <p className="text-xs text-slate-400 font-mono">Touch FIDO2 / WebAuthn security key to authorize action.</p>
                  </div>
                </div>

                <div className="bg-slate-950 p-4 rounded-xl border border-slate-800 font-mono text-xs flex flex-col gap-1">
                  <span className="text-slate-500 text-[10px]">TARGET ACTION</span>
                  <span className="text-rose-400 font-bold">{pendingAdminAction?.actionType}</span>
                </div>

                <div className="flex gap-3">
                  <button 
                    onClick={() => setWebAuthnPending(false)}
                    className="flex-1 bg-slate-800 hover:bg-slate-700 text-slate-300 font-mono text-xs py-2.5 rounded-xl border border-slate-700"
                  >
                    Cancel
                  </button>
                  <button 
                    onClick={handleWebAuthnVerify}
                    className="flex-1 bg-indigo-600 hover:bg-indigo-500 text-white font-mono text-xs font-bold py-2.5 rounded-xl shadow-lg shadow-indigo-600/20 flex items-center justify-center gap-2"
                  >
                    <ShieldCheck size={14} /> Verify FIDO2 Key
                  </button>
                </div>
              </div>
            </div>
          )}

          {/* Quorum Approvals Queue */}
          <div className="bg-slate-900 border border-slate-800 rounded-2xl p-5 flex flex-col gap-4">
            <div className="flex items-center justify-between border-b border-slate-800 pb-3">
              <div className="flex items-center gap-2">
                <UserCheck size={18} className="text-amber-400" />
                <h3 className="text-xs font-mono font-bold text-slate-200 uppercase tracking-wider">Dual-Control Quorum Approvals (Checker Queue)</h3>
              </div>
              <span className="text-[10px] font-mono text-amber-400 bg-amber-950 px-2 py-0.5 rounded border border-amber-800">
                {quorumRequests.length} PENDING
              </span>
            </div>

            <div className="flex flex-col gap-2 font-mono text-xs">
              {quorumRequests.map(req => (
                <div key={req.id} className="p-3 bg-slate-950 rounded-xl border border-slate-850 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-3">
                  <div>
                    <div className="flex items-center gap-2">
                      <span className="text-slate-400 font-bold">{req.id}</span>
                      <span className="text-slate-200 font-semibold">{req.action}</span>
                    </div>
                    <span className="text-[10px] text-slate-500">Maker: {req.maker} • {req.timestamp}</span>
                  </div>
                  <button 
                    onClick={() => initiateAdminStepUp('APPROVE_QUORUM', { reqId: req.id })}
                    className="bg-emerald-600/20 hover:bg-emerald-600/30 text-emerald-300 border border-emerald-500/30 px-3 py-1.5 rounded-lg text-xs font-bold transition-colors"
                  >
                    Approve (Checker)
                  </button>
                </div>
              ))}
              {quorumRequests.length === 0 && (
                <span className="text-slate-500 text-xs py-2">No pending approval requests in checker queue.</span>
              )}
            </div>
          </div>

          {/* SHA-256 Audit Ledger */}
          <div className="bg-slate-900 border border-slate-800 rounded-2xl overflow-hidden flex flex-col">
            <div className="bg-slate-950 px-6 py-4 border-b border-slate-800 flex items-center justify-between">
              <div className="flex items-center gap-2">
                <Database size={16} className="text-rose-400" />
                <span className="text-xs font-mono font-bold text-slate-200 uppercase">Cryptographic Audit Chain (SHA-256 Append-Only)</span>
              </div>
              <span className="text-[10px] font-mono text-slate-500">source: sandbox-mock</span>
            </div>

            <div className="p-4 overflow-x-auto bg-slate-950/60">
              <table className="w-full text-left font-mono text-xs border-collapse">
                <thead>
                  <tr className="border-b border-slate-800 text-slate-500 text-[10px] uppercase">
                    <th className="pb-2 px-2">ID</th>
                    <th className="pb-2 px-2">Timestamp</th>
                    <th className="pb-2 px-2">Actor</th>
                    <th className="pb-2 px-2">Action</th>
                    <th className="pb-2 px-2">SHA-256 Hash Digest</th>
                  </tr>
                </thead>
                <tbody className="divide-y divide-slate-800/40">
                  {unredactedLogs.map(log => (
                    <tr key={log.id} className="hover:bg-slate-900/40">
                      <td className="py-2.5 px-2 text-slate-400 font-bold">{log.id}</td>
                      <td className="py-2.5 px-2 text-slate-500 whitespace-nowrap">{log.timestamp}</td>
                      <td className="py-2.5 px-2 text-indigo-300">{log.actor}</td>
                      <td className="py-2.5 px-2 font-bold text-slate-200">{log.action}</td>
                      <td className="py-2.5 px-2 text-slate-500 text-[10px] truncate max-w-xs">{log.sha256}</td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
        </div>
      )}

    </main>
  </div>

  {/* Footer */}
  <footer className={classes.footer}>
    <div className="flex items-center gap-2 text-slate-400 font-mono">
      <Shield size={12} className="text-indigo-400" />
      <span>Apex Capital Web LLC • Edge Control Plane Boundary</span>
    </div>
    <div className="text-slate-500 font-mono">
      DISCLAIMER: NOT REGULATED, NOT CUSTODIAL. Sandbox only.
    </div>
  </footer>
</div>
);}![Windows Terminal project logos and branding image](https://github.com/microsoft/terminal/assets/91625426/333ddc76-8ab2-4eb4-a8c0-4d7b953b1179)

[![Terminal Build Status](https://dev.azure.com/shine-oss/terminal/_apis/build/status%2FTerminal%20CI?branchName=main)](https://dev.azure.com/shine-oss/terminal/_build/latest?definitionId=1&branchName=main)

# Welcome to the Windows Terminal, Console and Command-Line repo

<details>
  <summary><strong>Table of Contents</strong></summary>

- [Installing and running Windows Terminal](#installing-and-running-windows-terminal)
  - [Microsoft Store \[Recommended\]](#microsoft-store-recommended)
  - [Other install methods](#other-install-methods)
    - [Via GitHub](#via-github)
    - [Via Windows Package Manager CLI (aka winget)](#via-windows-package-manager-cli-aka-winget)
    - [Via Chocolatey (unofficial)](#via-chocolatey-unofficial)
    - [Via Scoop (unofficial)](#via-scoop-unofficial)
- [Installing Windows Terminal Canary](#installing-windows-terminal-canary)
- [Terminal \& Console Overview](#terminal--console-overview)
  - [Windows Terminal](#windows-terminal)
  - [The Windows Console Host](#the-windows-console-host)
  - [Shared Components](#shared-components)
  - [Creating the new Windows Terminal](#creating-the-new-windows-terminal)
- [Resources](#resources)
- [FAQ](#faq)
  - [I built and ran the new Terminal, but it looks just like the old console](#i-built-and-ran-the-new-terminal-but-it-looks-just-like-the-old-console)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [Communicating with the Team](#communicating-with-the-team)
- [Developer Guidance](#developer-guidance)
- [Prerequisites](#prerequisites)
- [Building the Code](#building-the-code)
  - [Building in PowerShell](#building-in-powershell)
  - [Building in Cmd](#building-in-cmd)
- [Running \& Debugging](#running--debugging)
  - [Coding Guidance](#coding-guidance)
- [Code of Conduct](#code-of-conduct)

</details>

<br />

This repository contains the source code for:

* [Windows Terminal](https://aka.ms/terminal)
* [Windows Terminal Preview](https://aka.ms/terminal-preview)
* The Windows console host (`conhost.exe`)
* Components shared between the two projects
* [ColorTool](./src/tools/ColorTool)
* [Sample projects](./samples)
  that show how to consume the Windows Console APIs

Related repositories include:

* [Windows Terminal Documentation](https://learn.microsoft.com/windows/terminal)
  ([Repo: Contribute to the docs](https://github.com/MicrosoftDocs/terminal))
* [Console API Documentation](https://github.com/MicrosoftDocs/Console-Docs)
* [Cascadia Code Font](https://github.com/Microsoft/Cascadia-Code)

## Installing and running Windows Terminal

> [!NOTE]
> Windows Terminal requires Windows 10 2004 (build 19041) or later

### Microsoft Store [Recommended]

Install the [Windows Terminal from the Microsoft Store][store-install-link].
This allows you to always be on the latest version when we release new builds
with automatic upgrades.

This is our preferred method.

### Other install methods

#### Via GitHub

For users who are unable to install Windows Terminal from the Microsoft Store,
released builds can be manually downloaded from this repository's [Releases
page](https://github.com/microsoft/terminal/releases).

Download the `Microsoft.WindowsTerminal_<versionNumber>.msixbundle` file from
the **Assets** section. To install the app, you can simply double-click on the
`.msixbundle` file, and the app installer should automatically run. If that
fails for any reason, you can try the following command at a PowerShell prompt:

```powershell
# NOTE: If you are using PowerShell 7+, please run
# Import-Module Appx -UseWindowsPowerShell
# before using Add-AppxPackage.

Add-AppxPackage Microsoft.WindowsTerminal_<versionNumber>.msixbundle
```

> [!NOTE]
> If you install Terminal manually:
>
> * You may need to install the [VC++ v14 Desktop Framework Package](https://learn.microsoft.com/troubleshoot/cpp/c-runtime-packages-desktop-bridge#how-to-install-and-update-desktop-framework-packages).
>   This should only be necessary on older builds of Windows 10 and only if you get an error about missing framework packages.
> * Terminal will not auto-update when new builds are released so you will need
>   to regularly install the latest Terminal release to receive all the latest
>   fixes and improvements!

#### Via Windows Package Manager CLI (aka winget)

[winget](https://github.com/microsoft/winget-cli) users can download and install
the latest Terminal release by installing the `Microsoft.WindowsTerminal`
package:

```powershell
winget install --id Microsoft.WindowsTerminal -e
```

> [!NOTE]
> Dependency support is available in WinGet version [1.6.2631 or later](https://github.com/microsoft/winget-cli/releases). To install the Terminal stable release 1.18 or later, please make sure you have the updated version of the WinGet client.

#### Via Chocolatey (unofficial)

[Chocolatey](https://chocolatey.org) users can download and install the latest
Terminal release by installing the `microsoft-windows-terminal` package:

```powershell
choco install microsoft-windows-terminal
```

To upgrade Windows Terminal using Chocolatey, run the following:

```powershell
choco upgrade microsoft-windows-terminal
```

If you have any issues when installing/upgrading the package please go to the
[Windows Terminal package
page](https://chocolatey.org/packages/microsoft-windows-terminal) and follow the
[Chocolatey triage process](https://chocolatey.org/docs/package-triage-process)

#### Via Scoop (unofficial)

[Scoop](https://scoop.sh) users can download and install the latest Terminal
release by installing the `windows-terminal` package:

```powershell
scoop bucket add extras
scoop install windows-terminal
```

To update Windows Terminal using Scoop, run the following:

```powershell
scoop update windows-terminal
```

If you have any issues when installing/updating the package, please search for
or report the same on the [issues
page](https://github.com/lukesampson/scoop-extras/issues) of Scoop Extras bucket
repository.

---

## Installing Windows Terminal Canary
Windows Terminal Canary is a nightly build of Windows Terminal. This build has the latest code from our `main` branch, giving you an opportunity to try features before they make it to Windows Terminal Preview.

Windows Terminal Canary is our least stable offering, so you may discover bugs before we have had a chance to find them.

Windows Terminal Canary is available as an App Installer distribution and a Portable ZIP distribution.

The App Installer distribution supports automatic updates. Due to platform limitations, this installer only works on Windows 11.

The Portable ZIP distribution is a portable application. It will not automatically update and will not automatically check for updates. This portable ZIP distribution works on Windows 10 (19041+) and Windows 11.

| Distribution  | Architecture    | Link                                                 |
|---------------|:---------------:|------------------------------------------------------|
| App Installer | x64, arm64, x86 | [Download](https://aka.ms/terminal-canary-installer) |
| Portable ZIP  | x64             | [Download](https://aka.ms/terminal-canary-zip-x64)   |
| Portable ZIP  | ARM64           | [Download](https://aka.ms/terminal-canary-zip-arm64) |
| Portable ZIP  | x86             | [Download](https://aka.ms/terminal-canary-zip-x86)   |

_Learn more about the [types of Windows Terminal distributions](https://learn.microsoft.com/windows/terminal/distributions)._

---

## Terminal & Console Overview

Please take a few minutes to review the overview below before diving into the
code:

### Windows Terminal

Windows Terminal is a new, modern, feature-rich, productive terminal application
for command-line users. It includes many of the features most frequently
requested by the Windows command-line community including support for tabs, rich
text, globalization, configurability, theming & styling, and more.

The Terminal will also need to meet our goals and measures to ensure it remains
fast and efficient, and doesn't consume vast amounts of memory or power.

### The Windows Console Host

The Windows Console host, `conhost.exe`, is Windows' original command-line user
experience. It also hosts Windows' command-line infrastructure and the Windows
Console API server, input engine, rendering engine, user preferences, etc. The
console host code in this repository is the actual source from which the
`conhost.exe` in Windows itself is built.

Since taking ownership of the Windows command-line in 2014, the team added
several new features to the Console, including background transparency,
line-based selection, support for [ANSI / Virtual Terminal
sequences](https://en.wikipedia.org/wiki/ANSI_escape_code), [24-bit
color](https://devblogs.microsoft.com/commandline/24-bit-color-in-the-windows-console/),
a [Pseudoconsole
("ConPTY")](https://devblogs.microsoft.com/commandline/windows-command-line-introducing-the-windows-pseudo-console-conpty/),
and more.

However, because Windows Console's primary goal is to maintain backward
compatibility, we have been unable to add many of the features the community
(and the team) have been wanting for the last several years including tabs,
unicode text, and emoji.

These limitations led us to create the new Windows Terminal.

> You can read more about the evolution of the command-line in general, and the
> Windows command-line specifically in [this accompanying series of blog
> posts](https://devblogs.microsoft.com/commandline/windows-command-line-backgrounder/)
> on the Command-Line team's blog.

### Shared Components

While overhauling Windows Console, we modernized its codebase considerably,
cleanly separating logical entities into modules and classes, introduced some
key extensibility points, replaced several old, home-grown collections and
containers with safer, more efficient [STL
containers](https://docs.microsoft.com/en-us/cpp/standard-library/stl-containers?view=vs-2022),
and made the code simpler and safer by using Microsoft's [Windows Implementation
Libraries - WIL](https://github.com/Microsoft/wil).

This overhaul resulted in several of Console's key components being available
for re-use in any terminal implementation on Windows. These components include a
new DirectWrite-based text layout and rendering engine, a text buffer capable of
storing both UTF-16 and UTF-8, a VT parser/emitter, and more.

### Creating the new Windows Terminal

When we started planning the new Windows Terminal application, we explored and
evaluated several approaches and technology stacks. We ultimately decided that
our goals would be best met by continuing our investment in our C++ codebase,
which would allow us to reuse several of the aforementioned modernized
components in both the existing Console and the new Terminal. Further, we
realized that this would allow us to build much of the Terminal's core itself as
a reusable UI control that others can incorporate into their own applications.

The result of this work is contained within this repo and delivered as the
Windows Terminal application you can download from the Microsoft Store, or
[directly from this repo's
releases](https://github.com/microsoft/terminal/releases).

---

## Resources

For more information about Windows Terminal, you may find some of these
resources useful and interesting:

* [Command-Line Blog](https://devblogs.microsoft.com/commandline)
* [Command-Line Backgrounder Blog
  Series](https://devblogs.microsoft.com/commandline/windows-command-line-backgrounder/)
* Windows Terminal Launch: [Terminal "Sizzle
  Video"](https://www.youtube.com/watch?v=8gw0rXPMMPE&list=PLEHMQNlPj-Jzh9DkNpqipDGCZZuOwrQwR&index=2&t=0s)
* Windows Terminal Launch: [Build 2019
  Session](https://www.youtube.com/watch?v=KMudkRcwjCw)
* Run As Radio: [Show 645 - Windows Terminal with Richard
  Turner](https://www.runasradio.com/Shows/Show/645)
* Azure DevOps Podcast: [Episode 54 - Kayla Cinnamon and Rich Turner on DevOps
  on the Windows
  Terminal](http://azuredevopspodcast.clear-measure.com/kayla-cinnamon-and-rich-turner-on-devops-on-the-windows-terminal-team-episode-54)
* Microsoft Ignite 2019 Session: [The Modern Windows Command Line: Windows
  Terminal -
  BRK3321](https://myignite.techcommunity.microsoft.com/sessions/81329?source=sessions)

---

## FAQ

### I built and ran the new Terminal, but it looks just like the old console

Cause: You're launching the incorrect solution in Visual Studio.

Solution: Make sure you're building & deploying the `CascadiaPackage` project in
Visual Studio.

> [!NOTE]
> `OpenConsole.exe` is just a locally-built `conhost.exe`, the classic
> Windows Console that hosts Windows' command-line infrastructure. OpenConsole
> is used by Windows Terminal to connect to and communicate with command-line
> applications (via
> [ConPty](https://devblogs.microsoft.com/commandline/windows-command-line-introducing-the-windows-pseudo-console-conpty/)).

---

## Documentation

All project documentation is located at [aka.ms/terminal-docs](https://aka.ms/terminal-docs). If you would like
to contribute to the documentation, please submit a pull request on the [Windows
Terminal Documentation repo](https://github.com/MicrosoftDocs/terminal).

---

## Contributing

We are excited to work alongside you, our amazing community, to build and
enhance Windows Terminal\!

***BEFORE you start work on a feature/fix***, please read & follow our
[Contributor's
Guide](./CONTRIBUTING.md) to
help avoid any wasted or duplicate effort.

## Communicating with the Team

The easiest way to communicate with the team is via GitHub issues.

Please file new issues, feature requests and suggestions, but **DO search for
similar open/closed preexisting issues before creating a new issue.**

If you would like to ask a question that you feel doesn't warrant an issue
(yet), please reach out to us via Twitter:

* Christopher Nguyen, Product Manager:
  [@nguyen_dows](https://twitter.com/nguyen_dows)
* Dustin Howett, Engineering Lead: [@dhowett](https://twitter.com/DHowett)
* Mike Griese, Senior Developer: [@zadjii@mastodon.social](https://mastodon.social/@zadjii)
* Carlos Zamora, Developer: [@cazamor_msft](https://twitter.com/cazamor_msft)
* Pankaj Bhojwani, Developer
* Leonard Hecker, Developer: [@LeonardHecker](https://twitter.com/LeonardHecker)

## Developer Guidance

## Prerequisites

You can configure your environment to build Terminal in one of two ways:

### Using WinGet configuration file

After cloning the repository, you can use a [WinGet configuration file](https://learn.microsoft.com/en-us/windows/package-manager/configuration/#use-a-winget-configuration-file-to-configure-your-machine)
to set up your environment. The [default configuration file](.config/configuration.winget) installs Visual Studio 2026 Community & rest of the required tools. There are two other variants of the configuration file available in the [.config](.config) directory for Enterprise & Professional editions of Visual Studio 2026. To run the default configuration file, you can either double-click the file from explorer or run the following command:

```powershell
winget configure .config\configuration.winget
```

### Manual configuration

* You must be running Windows 10 2004 (build >= 10.0.19041.0) or later to run
  Windows Terminal
* You must [enable Developer Mode in the Windows Settings
  app](https://learn.microsoft.com/windows/uwp/get-started/enable-your-device-for-development)
  to locally install and run Windows Terminal
* You must have [PowerShell 7 or later](https://github.com/PowerShell/PowerShell/releases/latest) installed
* You must have the [Windows 11 (10.0.26100) SDK](https://developer.microsoft.com/windows/downloads/windows-sdk/) installed at version 10.0.26100.8249 or greater.
* You must have at least [VS 2026](https://visualstudio.microsoft.com/downloads/) version 18.6 installed
* You must install the following Workloads via the VS Installer. Note: Opening
  the solution will [prompt you to install missing components automatically](https://devblogs.microsoft.com/setup/configure-visual-studio-across-your-organization-with-vsconfig/):
  * Desktop Development with C++
  * WinUI application development
* You must install the [.NET Framework 4.7.2 Targeting Pack](https://learn.microsoft.com/dotnet/framework/install/guide-for-developers#to-install-the-net-framework-developer-pack-or-targeting-pack) to build test projects

## Building the Code

OpenConsole.slnx may be built from within Visual Studio or from the command-line
using a set of convenience scripts & tools in the **/tools** directory:

### Building in PowerShell

```powershell
Import-Module .\tools\OpenConsole.psm1
Set-MsBuildDevEnvironment
Invoke-OpenConsoleBuild
```

### Building in Cmd

```shell
.\tools\razzle.cmd
bcz
```

## Running & Debugging

To debug the Windows Terminal in VS, right click on `CascadiaPackage` (in the
Solution Explorer) and go to properties. In the Debug menu, change "Application
process" and "Background task process" to "Native Only".

You should then be able to build & debug the Terminal project by hitting
<kbd>F5</kbd>. Make sure to select either the "x64" or the "x86" platform - the
Terminal doesn't build for "Any Cpu" (because the Terminal is a C++ application,
not a C# one).

> 👉 You will _not_ be able to launch the Terminal directly by running the
> WindowsTerminal.exe. For more details on why, see
> [#926](https://github.com/microsoft/terminal/issues/926),
> [#4043](https://github.com/microsoft/terminal/issues/4043)

### Coding Guidance

Please review these brief docs below about our coding practices.

> 👉 If you find something missing from these docs, feel free to contribute to
> any of our documentation files anywhere in the repository (or write some new
> ones!)

This is a work in progress as we learn what we'll need to provide people in
order to be effective contributors to our project.

* [Coding Style](./doc/STYLE.md)
* [Code Organization](./doc/ORGANIZATION.md)
* [Exceptions in our legacy codebase](./doc/EXCEPTIONS.md)
* [Helpful smart pointers and macros for interfacing with Windows in WIL](./doc/WIL.md)

---

## Code of Conduct

This project has adopted the [Microsoft Open Source Code of
Conduct][conduct-code]. For more information see the [Code of Conduct
FAQ][conduct-FAQ] or contact [opencode@microsoft.com][conduct-email] with any
additional questions or comments.

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[store-install-link]: https://aka.ms/terminal
