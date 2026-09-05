
## 1. Project Overview
Project video instruction: https://drive.google.com/drive/u/3/folders/1PD6DXG3IR1JZiU4XOAe0n_gfzrgM0ejG

Field Service Work Order System
Project Overview
Ei project ta Oracle APEX (22.1.0) and  Oracle Database(Oracle Databse 19css) diye develop kora ekta Field Service Work Order Management System. System-e Engineer, Dispatcher ebong Manager role ache. Main focus holo business rules gulo database level-e enforce kora, jate direct SQL diyeo invalid operation kora na jay.
1. Database / ERD Description
Main table gulo:
• XH_USERS – User ebong role information.
• XH_CUSTOMERS – Customer information.
• XH_WORK_ORDERS – Main Work Order information.
• XH_PARTS – Parts information.
• XH_WORK_ORDER_PARTS – Work Order-er used parts.
• XH_VAN_STOCKS – Engineer van-er stock.
• XH_SLA_PRIORITIES – Priority based SLA.
• XH_HOLIDAYS – Holiday information.
• XH_CONFIG_THRESHOLDS – Approval threshold.
• XH_WORK_ORDER_AUDITS – Status change audit.
• XH_STOCK_MOVEMENT_AUDITS – Stock movement audit.

Main relationship: Customer → Work Order → Engineer -> Work Order → Work Order Parts → Parts.
2. Seven Business Rules
Rule 1 – Lifecycle: NEW → ASSIGNED → IN PROGRESS → COMPLETED → CLOSED. ON HOLD flow ebong CANCELLED rules database trigger diye enforce kora hoyeche. Invalid transition, jemon NEW → COMPLETED, block kora hoy.

Rule 2 – No Double Booking: Same Engineer-er overlapping Work Order prevent korar jonno database-level locking/concurrency approach design kora hoyeche.

Rule 3 – SLA: Priority based SLA structure ache incomplete. Business hours, holiday ebong ON HOLD pause-er full implementation ekhono baki.

Rule 4 – Parts/Stock: Work Order-e Parts add/update system implement kora hoyeche.  

Rule 5 – Approval: Parts cost 300(Database theke asbe ai value)-er beshi hole Manager approval lagbe. APPROVAL_STATUS, APPROVED_BY, APPROVED_THRESHOLD, APPROVAL_TIME add kora hoyeche. XH_APPROVE_WORK_ORDER create kora hoyeche.

Rule 6 – Audit: Work Order status change XH_WORK_ORDER_AUDITS-e record hoy. Stock movement-er complete audit ekhono baki.

Rule 7 – Reopen: CLOSED Work Order 7 diner moddhe Manager reopen kore linked follow-up Work Order create korbe. Ei feature ekhono implement hoyni.(ata korte pari nai)
3. APEX Pages
Page 4 – Work Orders Report: Work Order list/report ebong Page 5-e navigation.

Page 5 – Work Order Details: Customer, Status, Priority, Engineer, Schedule, Approval Status, Total Parts Cost ebong Parts Used Interactive Grid ache. Engineer-er jonno Complete Work Order button ebong Manager approval flow-er foundation create kora hoyeche.
4. Packages
PKG_XH_INVENTORY – Parts related operation.
Procedure: XH_ASSIGN_ENGINEER– Engineer Work Order operation; COMPLETE_WORK_ORDER ai procedure a manage kora ace, final stock/approval transaction baki.
 Procedure: XH_APPROVE_WORK_ORDER  – Manager approval-er jonno APPROVE_WORK_ORDER 
5. REST / Duplicate Prevention
REST endpoint ekhono fully complete hoyni. Planned approach holo database-level unique partner reference/idempotency key use kora, jate concurrent retry-te duplicate Work Order create na hoy. Advanced option final select kora baki.
6. Performance / Execution Plan
Assessment-er jonno 250k+ Work Order data, heavy query-er execution plan ebong <2 second search performance test korte hobe. Egulo ekhono final kora hoyni. Ami sudhu dumy data insert korehi and dekheci load time ta Kemon somoy ney.
7. Environment
Oracle APEX: 22.1.0
Oracle Database Version:  Oracle Database 19 c
8. Unfinished Work
• Final completion  
• Pdf Report Design.
• Negative stock prevention + full stock movement audit
• SLA/business calendar use kora.
 • CLOSED Work Order reopen/follow-up
• REST endpoint + idempotency/concurrency testing
• Advanced option
• 250k+ seed data
• Performance testing
• Final security 
• Dashboard Design
9. Least-Confidence Decisions
1. Final REST advanced option.(REST API use korete parbo)
2. Dashboard Design as per requirement and PDF Report Design using BI Publisher.
2. Offline capture and sync.
3. Final stock movement audit data model.
10. AI Tool Usage

AI tools requirement analysis,   design concept improve,Procedure Fucntion Login Improve, concurrency/approval logic, troubleshooting ebong documentation-e development assistant hisebe use kora hoyeche. Suggestions review kore implementation kora hoyeche.
I use AI as a assistant . 
Current Project Status
Database structure, authorization, Work Order lifecycle, audit, APEX Report, Work Order Details, Parts management ebong Manager Approval foundation implement kora hoyeche. Main remaining work holo final business transaction logic, stock, SLA, REST, performance testing ebong final deployment/documentation.
Requirments er main part (Work order manage ) ata niye ami besi focus korechi.
