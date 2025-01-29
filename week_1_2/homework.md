# Question 1
```bash
docker run --entrypoint bash -it python:3.12.8
pip --version
```
# Question 2

    db is the name of the service, and the port 5432 is the port that is on the container, which maps to the port 5433 on the host machine.

# Question 3

```sql
select count(*)
from green_taxi_data
where (lpep_dropoff_datetime >= '2019-10-01' and lpep_dropoff_datetime < '2019-11-01')
and trip_distance > 1.00;
```

```sql
select count(*)
from green_taxi_data
where (lpep_dropoff_datetime >= '2019-10-01' and lpep_dropoff_datetime < '2019-11-01')
and (trip_distance > 1.00 and trip_distance <= 5.00);
```

```sql
select count(*)
from green_taxi_data
where (lpep_dropoff_datetime >= '2019-10-01' and lpep_dropoff_datetime < '2019-11-01')
and (trip_distance > 5.00 and trip_distance <= 7.00);
```

```sql
select count(*)
from green_taxi_data
where (lpep_dropoff_datetime >= '2019-10-01' and lpep_dropoff_datetime < '2019-11-01')
and (trip_distance > 7.00 and trip_distance <= 10.00);
```

```sql
select count(*)
from green_taxi_data
where (lpep_dropoff_datetime >= '2019-10-01' and lpep_dropoff_datetime < '2019-11-01')
and trip_distance > 10.00;
```

# Question 4

```sql
select lpep_pickup_datetime
from green_taxi_data
where lpep_pickup_datetime >= '2019-10-01' and lpep_pickup_datetime < '2019-10-02'
or lpep_pickup_datetime >= '2019-10-24' and lpep_pickup_datetime < '2019-10-25'
or lpep_pickup_datetime >= '2019-10-26' and lpep_pickup_datetime < '2019-10-27'
or lpep_pickup_datetime >= '2019-10-31' and lpep_pickup_datetime < '2019-11-01'
group by lpep_pickup_datetime
order by max(trip_distance) desc
limit 1;
```

# Question 5

```sql
select "Zone"
from zones
join (
	select "PULocationID"
	from green_taxi_data
	where (lpep_pickup_datetime >= '2019-10-18' and lpep_pickup_datetime < '2019-10-19')
	group by "PULocationID"
	having sum(total_amount) > 13000
	order by sum(total_amount) desc
    ) as loc
on zones."LocationID" = loc."PULocationID";
```

# Question 6

```sql
select "Zone"
from zones
join (select "DOLocationID"
	from green_taxi_data
	where "PULocationID" = (
		select "LocationID"
		from zones
		where "Zone" = 'East Harlem North'
		)
	and (lpep_pickup_datetime >= '2019-10-01' 
		and lpep_pickup_datetime < '2019-11-01')
	group by "DOLocationID"
	order by max(tip_amount) desc
	limit 1) as loc
on zones."LocationID" = loc."DOLocationID";
```

# Question 7
```terraform
terraform init
terraform plan
terraform apply
terraform destroy
```