## BoloSQL_dev.dbo.tbl_glosf_detail

### Creation Script
NONE

### Update Script
BoloSQL_dev.dbo.sp_los_build_glosf <br>
Lines 35 to 86

### Comments: 
bolosql_prod.dbo.trans is filtered on inner join of bolosql_dev.dbo.vw_bc_coa_grps where (acct_grp_catgy = 'LOSG').

![system overview](http://www.plantuml.com/plantuml/proxy?cache=no&src=https://raw.github.com/CKronkosky/DW-01.BoloSQL_Dev/master/docs/diagrams/src/bolosql_dev.dbo.tbl_glosf_detail.puml)

``` sql
truncate table bolosql_dev.dbo.tbl_glosf_detail

insert into bolosql_dev.dbo.tbl_glosf_detail (
  u2_id
, acct
, incl_acct_plain
, acct_name
, acctg_period
, activity_date
, price_oil
, price_gas
, price_ngl
, app
, company
, [description]
, stat1_amt
, stat1_qty1
, fincat
, fincat_desc
, losid
, los_desc
, loslinetxt
, losline
, lostype
, cost_center
, shadow_key
, cc_type
, category
, cc_name
, acquisition
, acq_descr
, eff_date
, acq_summ_grp
, fieldname
, [state]
, county_name
, operator
, oper_name
, prop_type
, lease_shadow
, lease_cc_name
, area_cc_name
, fmn_cc_name
, eng_cc_name
, supt_cc_name
, op_cc_name
, co_cc_name
, vendor
, vendor_name
, project
, source_document
, source_table
, system_date
, system_user_id
, curr_status
, doi
, doi_session
, product
, cnv_id
, [type]
, voucher
, appr
, appr_date
, time_stamp
, direct_bill
, jib_deck
, jib_deck_session
, jib_alloc_date
, src_alloc_trans_id
, cc_alloc_date
, cc_alloc_id
, alloc_enabled
, alloc_pct
, fieldid
, distr
, region
, image_ref
, [file_id]
, image_link
, supt2
, mgmt_rollup
)
select 
  a.u2_id
, a.acct
, cc.incl_acct_plain
, b.acct_name
, a.acctg_period
, a.activity_date
, 0 as price_oil
, 0 as price_gas
, 0 as price_ngl
, a.app
, a.company
, a.description
, case when substring(cc.acct_grp,6,1) = '0' then convert(decimal(14,2),a.stat1_amt*-1) 
       else convert(decimal(14,2),a.stat1_amt) 
  end as stat1_amt
, case when substring(cc.acct_grp,6,1) = '0' then convert(decimal(14,2),a.stat1_qty1*-1) 
       else convert(decimal(14,2),a.stat1_qty1) 
  end as stat1_qty1
, c.acct_grp as fincat
, c.acct_grp_desc as fincat_desc
, cc.acct_grp as losid
, cc.acct_grp_desc as los_desc
, substring(cc.acct_grp,6,20) as loslinetxt
, convert(float,null) as losline
, 'glosf' as lostype
, a.cost_center
, d.shadow_key
, d.cc_type
, d.category
, d.cc_name
, isnull(dd.acquisition,'(NONE)') as acquisition
, isnull(dd.acq_descr,'(NONE)') as acq_descr
, isnull(dd.eff_date,'1/1/2005') as eff_date
, isnull(dd.acq_summ_grp,'(NONE)') as acq_summ_grp
, isnull(dd.fieldname,'(NONE)') as fieldname
, dd.state
, dd.county_name
, isnull(dd.operator,'(NONE)') as operator
, isnull(dd.oper_name,'(NONE)') as oper_name
, dd.prop_type
, isnull(dd.lease_shadow,'(NONE)') as lease_shadow
, isnull(dd.lease_cc_name,'(NONE)') as lease_cc_name
, isnull(dd.area_cc_name,'(NONE)') as area_cc_name
, isnull(dd.fmn_cc_name,'(NONE)') as fmn_cc_name
, isnull(dd.eng_cc_name,'(NONE)') as eng_cc_name
, isnull(dd.supt_cc_name,'(NONE)') as supt_cc_name
, isnull(dd.op_cc_name,'(NONE)') as op_cc_name
, isnull(dd.co_cc_name,'(NONE)') as co_cc_name
, a.name as vendor
, e.name1 as vendor_name
, a.project
, a.source_document
, a.source_table
, a.system_date
, a.system_user_id
, a.curr_status
, a.doi
, a.doi_session
, a.product
, a.cnv_id
, a.type
, a.voucher
, f.appr
, f.appr_date
, a.time_stamp
, a.direct_bill
, a.jib_deck
, a.jib_deck_session
, a.jib_alloc_date
, a.src_alloc_trans_id
, a.cc_alloc_date
, a.cc_alloc_id
, a.alloc_enabled
, a.alloc_pct
, dd.fieldid
, dd.distr
, dd.region
, g.image_ref
, h.[file_id]
, image_link = case when h.[file_id] is null then null 
                    else 'http://docvueent/direct?q=query%3D((doc-id)eq(' + 
                         h.[file_id] + 
                         '))%26sort%3Ddoc-id%26order%3Dasc%26latestVersion%3Dtrue%26appid%3D2&app=2&sp=29&u=1014&type=launch' 
  end
, isnull(dd.supt2,'(NONE)') as supt2
, isnull(dd.mgmt_rollup,'(NONE)') as mgmt_rollup
from bolosql_prod.dbo.trans a
left join bolosql_dev.dbo.vw_bc_coa b on a.acct = b.acct_id
left join (
  select * 
  from bolosql_dev.dbo.vw_bc_coa_grps 
  where acct_grp_catgy = 'FC'
) c on a.acct = c.incl_acct
join (
  select * 
  from bolosql_dev.dbo.vw_bc_coa_grps 
  where acct_grp_catgy = 'LOSG'
) cc on a.acct = cc.incl_acct
left join bolosql_dev.dbo.vw_bc_prop_cc_master d on a.cost_center = d.u2_id
left join bolosql_dev.dbo.tbl_bc_PropertyMaster dd on a.cost_center = dd.u2_id
left join bolosql_prod.dbo.name e on a.name = e.u2_id
left join bolosql_prod.dbo.voucher f on a.voucher = f.u2_id
left join bolosql_prod.dbo.ap_inv g on a.source_document = g.u2_id
left join bolosql_prod.dbo.document h on g.image_ref = h.u2_id
where f.appr_date is not null and 
      a.acctg_period >= '1/1/11' and	--exclude converted data; to do converted data one-time, seperate
      a.acct NOT IN ('145..150','152..600','153..600','154..600','154..650','154..700','154..700','157..600','158..600') and --Added per Micah as these should not be on the LOS
      isnull(a.source_document,'') not in ('PL.CLOSING', 'P&L') and 
      a.company = '601' and 
      a.[type] not like 'JB%' and 
      a.stat1_amt is not null

delete from bolosql_dev.dbo.tbl_glosf_detail
where (stat1_amt between -.009 and .009 and isnull(stat1_qty1,0) between -.009 and .009)	-- -- delete zero amount lines

update bolosql_dev.dbo.tbl_glosf_detail
set losline = convert(float,loslinetxt)
```
