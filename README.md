# SQL Challenge

## Credentials

type: postgresql 

hostname: dstest.cyio0b3wel6y.us-east-1.rds.amazonaws.com

port: 5432 

username: dscandidate 

password: <removed> 

database: dstest 

URL for scraping section:
http://ec2-54-90-234-76.compute-1.amazonaws.com/docstars_pg1.html

# Questions:

`How many providers does each group have?`


### Questions 1

`How many primary care providers?`

```sql

select
	medical_group_id,
	count(distinct npi) as distinct_provider_count,
	count(*) as non_distinct_provider_count -- sanity check
from
	directory.provider_groups
group by
	medical_group_id
	
```

```
medical_group_id	distinct_provider_count	non_distinct_provider_count
029fc58de74cc766fe41649e54f39400	10	10
088bd4b0e5e0edf718e990bf39fec887	3	3
17b7cdcd78be5aa1504eb662b16ea743	3	3
1a81f1eed6f1dcfb29345145abe19413	6	6
1bb7237aa66907ad613dc4b58e7ffbc2	8	8
1cbf5b417386e0ce676513fec9a878d4	7	7
1debbe5ad03b894e035094bed85a7c25	1	1
261c54cad6ac3b9d7847b7ae11b712ac	1	1
267bc253248d5924bd68e050948f2741	4	4
2ca690a44e0cf70b189bcbb18eeed695	1	1
2da3e6cb4f4a4c3c563a4a9e8d7220ad	1	1
2e03e636383536ed655ca71d0f5d0ca8	10	10
4178f10fd30f855dcb26b0730b48f61e	1	1
4c129060a7ef7b9f9d078c9fb33af4ee	3	3
4e46eb0698ad4360433a927bd3c4660e	1	1
57646943faf2f9448a85b4e01aba8f7f	1	1
60919a9d0c0fe0930b5652eab4ea0087	1	1
635e40654456c4c350e35f71e626326d	8	8
721c30b910cbf7094e6c419421e93f86	1	1
7af7792a7d006953d78625abcbc702f1	3	3
7b8afb76081ac6268271201444e4ade2	1	1
7d6142430f8fee2fd6351518bc9d115e	5	5
8751a914a8dff64f63be0af6e5c801eb	2	2
934ab6f68a037fe4b5471031b72b072b	6	6
95c9b9061958605fb247eb1aef43ead0	4	4
b23188dbe1f0dff437b87a4b87223626	7	7
b26f2cf050b1147c3f7bdb5ac3a2a6ad	1	1
c6982433a17952c22c86dc5ce58dd87a	6	6
c924d2a8323e4c593f86557ff20d83a0	2	2
cbd7db9111ab29f5ba622f4ae6de053b	1	1
da0bd0afed2d54aac6c7f161a4364fdb	5	5
dbe45a3d7b44fc5ae5038e45730f2c7a	1	1
dde2eca45851abae232c627ed2a8a377	3	3
f3ff2018ae06426f50a38a1067fd877f	3	3
fa150652606d594f2ff4174e56d0845d	3	3
ff3988214581c6a1defcf8b4f68fbd1b	1	1
```

`How many primary care providers?`

```sql
select
	medical_group_id,
	count(distinct pg.npi) as distinct_provider_count,
	count(distinct case when is_pcp is true then p.npi else null end) as distinct_primary_care_providers 
from
	directory.provider_groups as pg
inner join directory.providers as p
on pg.npi = p.npi
group by
	medical_group_id
```

```sqlmedical_group_id	distinct_provider_count	distinct_primary_care_providers
029fc58de74cc766fe41649e54f39400	10	4
088bd4b0e5e0edf718e990bf39fec887	3	1
17b7cdcd78be5aa1504eb662b16ea743	3	0
1a81f1eed6f1dcfb29345145abe19413	6	1
1bb7237aa66907ad613dc4b58e7ffbc2	8	2
1cbf5b417386e0ce676513fec9a878d4	7	0
1debbe5ad03b894e035094bed85a7c25	1	0
261c54cad6ac3b9d7847b7ae11b712ac	1	0
267bc253248d5924bd68e050948f2741	4	3
2ca690a44e0cf70b189bcbb18eeed695	1	1
2da3e6cb4f4a4c3c563a4a9e8d7220ad	1	1
2e03e636383536ed655ca71d0f5d0ca8	10	5
4178f10fd30f855dcb26b0730b48f61e	1	0
4c129060a7ef7b9f9d078c9fb33af4ee	3	1
4e46eb0698ad4360433a927bd3c4660e	1	0
57646943faf2f9448a85b4e01aba8f7f	1	0
60919a9d0c0fe0930b5652eab4ea0087	1	0
635e40654456c4c350e35f71e626326d	8	0
721c30b910cbf7094e6c419421e93f86	1	0
7af7792a7d006953d78625abcbc702f1	3	0
7b8afb76081ac6268271201444e4ade2	1	0
7d6142430f8fee2fd6351518bc9d115e	5	0
8751a914a8dff64f63be0af6e5c801eb	2	0
934ab6f68a037fe4b5471031b72b072b	6	0
95c9b9061958605fb247eb1aef43ead0	4	0
b23188dbe1f0dff437b87a4b87223626	7	0
b26f2cf050b1147c3f7bdb5ac3a2a6ad	1	0
c6982433a17952c22c86dc5ce58dd87a	6	2
c924d2a8323e4c593f86557ff20d83a0	2	0
cbd7db9111ab29f5ba622f4ae6de053b	1	0
da0bd0afed2d54aac6c7f161a4364fdb	5	0
dbe45a3d7b44fc5ae5038e45730f2c7a	1	0
dde2eca45851abae232c627ed2a8a377	3	0
f3ff2018ae06426f50a38a1067fd877f	3	0
fa150652606d594f2ff4174e56d0845d	3	1
ff3988214581c6a1defcf8b4f68fbd1b	1	1
```

### Questions 2

`2. Which providers do not have associated contact info (order the list by NPI and include the top 20 results)?`

```sql
	
-- Option 1 	
select p.*
from directory.providers as p
left outer join directory.provider_contact_info as pci
on p.npi = pci.npi 
where pci.npi is null
order by p.npi
limit 20
```
```sql
-- Sanity check different way

select * from directory.providers as p 
where p.npi not in (select distinct npi from directory.provider_contact_info)
order by p.npi
limit 20

```

```
npi	full_name	is_pcp
1003868902	MARK ALAN WHITING	true
1124069992	ESTEBAN MARTIN KLOOSTERMAN	false
1184982993	KERRY-ANN D MILLER	true
1225041163	MARISA F. BAKER	false
1295936920	DANIEL LAWRENCE COHEN	false
1336143676	PAUL RICHARD WILLIAMSON	false
1487843504	MARSHA SHAWN ZERO	false
1508879123	HOWARD S GILL	false
1659356129	ALEXIS JOSE BECEIRO	false
1669478087	VINCENT G CARIFI	false
1720287659	ABIE ALIAS SAMUEL	false
1871589416	LYLE CRAIG FEINSTEIN	false
1942658174	FELIPE  LUGO	true
1982756821	ALEX  IGLESIAS	false
```

### Question 3
   
`The provider_contact_info table contains contact information from many different data sources with different levels of confidence and recency. Using these data:`

### Question 3a

`For each provider, find the record associated with the most recent update (order the list by NPI and include the top 20 results)`


```sql
--- Find the most recent contact update for each provider
select
	pci.*
from
	directory.provider_contact_info as pci
inner join (
	select
		npi,
		max(update_date) as last_update_date
	from
		directory.provider_contact_info
	group by
		npi ) as pci_last_update_date
on pci.npi = pci_last_update_date.npi
	and pci.update_date = pci_last_update_date.last_update_date
order by
	pci.npi
limit 20
```

```
npi	address1	address2	city	state	zip	phone	fax	data_source	confidence_score	update_date
1003872375	8391 W Oakland Park Blvd		Sunrise	FL	33351	9547492184		F	0.0168107376	2018-07-22
1013183425	6900 SW 80th St		Miami	FL	33143	7866628531	7866624649	C	0.1572084353	2018-08-14
1023038494	3450 Lantana Rd		Lake Worth	FL	33462	5619651864	5619675005	C	0.5102378076	2018-08-08
1023120664	5405 Okeechobee Blvd	Unit 100	West Palm Beach	FL	33417	5614208490	5614208491	E	0.6812143236	2018-07-06
1023440989	293 NW Peacock Blvd		Port St. Lucie	FL	34986	7723560114		F	0.0051682806	2018-08-19
1033180500	1600 Lakeland Hills Blvd		Lakeland	FL	33805	8636807000	8662648519	E	0.1097760709	2018-08-14
1043462211	1706 E Semoran Blvd	Unit 101	Apopka	FL	32703	4078809631		C	0.2983583469	2018-07-06
1053303263	1495 W State Rd 434		Longwood	FL	32750	4073328255	4073325769	C	0.1254609614	2018-07-19
1073532677	1 Tampa General Cir		Tampa	FL	33606	8139743113	8139745536	C	0.5319232617	2018-07-22
1073558300	5701 Overseas Hwy		Marathon	FL	33050	3053402312	3057432765	C	0.0679334877	2018-07-09
1083604136	7100 W 20th Ave		Hialeah	FL	33016	3055573212	3055573261	E	0.8614161102	2018-08-25
1083682496	621 Lumsden Professional Ct		Brandon	FL	33511	8136574103	8136574003	C	0.0277407165	2018-08-22
1104914704	5301 S Congress Ave		Lake Worth	FL	33462	5619657300	8569688239	E	0.4239802721	2018-08-19
1114195260	14601 SW 29th St		Miramar	FL	33027	9544140090	9544996646	A	0.6010211718	2018-07-11
1144282641	9159 SW 87th Ave		Miami	FL	33176	3052792499	3052796647	C	0.0987745282	2018-08-19
1144583899	1900 Don Wickham Dr		Clermont	FL	34711	3525368840	3525368841	C	0.2892932139	2018-08-06
1164421301	1071 S Sun Dr		Lake Mary	FL	32746	4073331616	4073331617	E	0.209059313	2018-08-13
1164483301	600 University Blvd		Jupiter	FL	33458	5618392780	5613540741	C	0.3207228497	2018-08-11
1164650016	1150 Campo Sano Ave		Coral Gables	FL	33146	7862686200	7865339977	E	0.3969778034	2018-08-21
1164650016	1150 Campo Sano Ave		Coral Gables	FL	33146	5618040679		C	0.0065024849	2018-08-21
```



### Question 3b

`For each provider, find the record associated with the highest quality source that has been updated in the last 60 days (order the list by NPI and include the top 20 results)`

*NOTE:*This question will go stale unless the data is refreshed for new candidates.

```sql

select npi,max(update_date)
from directory.provider_contact_info
where update_date >= now() - interval '60 day'
group by npi

```

There are no records that have been edited in the last 60 days. 

`0 records`

BUT I'm assuming this might be a mistake, so the query to find the records if they existed would look like:

```sql

select
	pci.*
from
	directory.provider_contact_info as pci
inner join (
	select
		npi,
		max(confidence_score) as highest_confidence
	from
		directory.provider_contact_info
	where update_date >= now() - interval '60 day'
	group by
		npi ) as pci_highest_recent_confidence
on pci.npi = pci_highest_recent_confidence.npi
	and pci.confidence_score = pci_highest_recent_confidence.highest_confidence
order by
	pci.npi
limit 20

```

Note: the query above assumes unique confidence scores. I'd need more clarification about how to handle ties, but in this case we'd return both results.

### Question 3c

`For each provider/data source combination, find the current phone number, previous phone number, and flag whether the number has changed`

```sql
select
	npi,
	data_source,
	update_date,
	phone,
	prev_phone,
	phone_changed
from
	(
	select
		npi,
		data_source,
		update_date,
		phone,
		lag(phone) over (partition by npi,
		data_source
	order by
		update_date) as prev_phone,
		case
			when phone != lag(phone) over (partition by npi,
			data_source
		order by
			update_date) then true
			else false
		end as phone_changed,
		rank() over (partition by npi,
		data_source
	order by
		update_date desc) as update_rank
	from
		directory.provider_contact_info as pci ) as full_update_list
where
	update_rank = 1
order by
	npi, data_source
limit 20
```

```npi	data_source	update_date	phone	prev_phone	phone_changed
1003872375	E	2018-05-20	9547491616	[NULL]	false
1003872375	F	2018-07-22	9547492184	9547491616	true
1013183425	B	2018-08-01	7866628118	[NULL]	false
1013183425	C	2018-08-14	7866628531	7864675701	true
1013183425	E	2018-06-09	7866628531	[NULL]	false
1023038494	A	2018-06-16	5619651864	[NULL]	false
1023038494	B	2018-08-06	5619651864	[NULL]	false
1023038494	C	2018-08-08	5619651864	[NULL]	false
1023038494	D	2018-05-31	5619651864	[NULL]	false
1023038494	E	2018-08-04	5619651864	[NULL]	false
1023120664	A	2018-06-11	5614208490	5614208490	false
1023120664	C	2018-06-03	5614208490	[NULL]	false
1023120664	E	2018-07-06	5614208490	[NULL]	false
1023440989	B	2018-08-10	7723359884	7723359600	true
1023440989	C	2018-05-14	7723359600	[NULL]	false
1023440989	D	2018-07-11	7723359600	7723359922	true
1023440989	F	2018-08-19	7723560114	7723359600	true
1033180500	A	2018-07-29	8636807000	[NULL]	false
1033180500	C	2018-05-22	8636807000	[NULL]	false
1033180500	E	2018-08-14	8636807000	[NULL]	false
```


# Phone Cleaning

`1508879123,35-871-3131` is a 9 digit phone number. Possibly valid in some countries. Skipped this one.

Also a malfored record, `1083682496,813-657-499` was skipped.

Have to deal with `1` or `+1` country code strings (like `+1 786.596.6743`). Also have to not include extension information in the base string, like (`(305) 913-1658 ext. 13`).

My choice of (simple) parsing would break if the phone numbers contained commas. We'd use a more robust library in practice and include unit tests to make sure we cover those edge-cases.

See `phone_cleaning.html` or `phone_cleaning.ipynb` for details.

# Data Scraping

See `data_scraping.html` or `data_scraping.ipynb` for details.

# Closing Notes:

This exercise took 5 hours. Several of the questions were ambiguous. The exercise didn't include context about what the intent was - given the scope of the work it isn't reasonable to expect well designed, idiomatic and tested code.