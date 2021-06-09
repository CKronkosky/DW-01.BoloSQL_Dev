## bolosql_prod.dbo.trans

| Type | Description |
| --- | --- |
| IC1 | from intercompany |
| IC2 | to intercompany |
| BAL | balancing interest |
| D | detail transactions |
| O | offset transactions |
| CR | Cash receipts (O&G sales & on acct) |
| CN1 | Partnership allocation txns |
| CN2 | Prtnrshp target company balancing txns |
| CN3 | Prtnrshp fully contrib invst grp txns |
| JB1.1 | Insider net cutback transactions |
| JB1.2 | Insider 8/8's cutback transactions |
| JB1.3 | Implied gain/loss on Non-WP MT |
| JB1.4 | Implied Gain/loss WP MT transactions  |
| JB1.5 | Implied loss on BB transaction |
| JB1.3R, JB1.4R, JB1.5R | reversals of JB1.3,JB1.4 and JB1.5  |
| JB2 | Billed to outsiders |
| JB3 | Deleted Interest |
| JB4 | Tsfr from unbilled to billed rcvbl |
| JB5 | Tsfr susp from unbilled to susp |
| JB6 | Tsfr from susp to unbilled |
| JB7 | Tsfr from unbilled to rev pybl (net) - JB7 is NOT USED! |
| JB8 | Tsfr from 8/8's acct to undist susp - JB8 not yet implemented!|
| JB9 | Tsfr from undist susp to 8/8's acct - JB9 not yet implemented! |
| RV | Clearing writeoff transactions |
| RV2.1 | Insider net cutback trans |
| RV2.2 | Insider 8/8's cutback trans |
| RV3 | Transfer from rev clrg to rev pybl |
| RV4 | Record agency payables |
| RV5 | Transfer from rev payable to suspense |
| RV6 | Transfer from suspense to rev pybl |
| RV7 | Transfer from rev payable to billed A/R |
| RV8 | Record pymt of rev payable |
| RV9 | Record rcvbl for tax w/h by purch remit by company |
| RV10 | Record write off of owner sale records |
| RV11 | Record gov royalty payable |
| RV1A | Record accrued sale |
| RV2A | Record accrued insider cutback transactions |
| RV3A | Transfer from accrued clearing to accrued O&G owner payable |
| RV4A | Record agency payables |
| BFW | 8/8's Balance forward transactions |
| G | gain/loss transactions (p406) 
| PTR | Clearing writeoff transactions |
| PTR2 | Insider net cutback trans |
| PTR3 | Transfer from ptr clrg to ptr pybl |
| PTR5 | Transfer from ptr payable to suspense |
| PTR6 | Transfer from suspense to ptr pybl |
| SUM.OFFSET | Summarization Offset |
| CC.AL.SUMMARY | Cost Center Allocation Summarization |
| PL.D | Profit and Loss Detail |
| PL.O | Profit and Loss Offset |
