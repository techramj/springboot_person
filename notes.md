
#Step 1: create the folder WEB-INF
create the folder WEB-INF as src/main/webapp/WEB-INF

#Step 2: create the folder jsps or views inside WEB-INF


#Step 3: configure the view resolver
* spring.mvc.view.prefix=/WEB-INF/views/
* spring.mvc.view.suffix=.jsp


#step 4: Enable the jsp support in embedded tomcat server

        <dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
			<scope>provided</scope>
		</dependency>


#step 5: Add the jstl dependency

		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>
		
#step 6: Add the logs
#Logging
#level Trace<Debug<Info<Error<Fatal
	logging.level.com.example=debug
	logging.level.org.springframework=debug



#step 7: spring JPA configuration
	#spring jpa datasource configuration
	#spring.datasource.driver-class-name=org.h2.Driver
	spring.datasource.driverClassName=org.h2.Driver
	spring.datasource.url=jdbc:h2:mem:db
	spring.datasource.username=sa
	spring.datasource.password=
	
	
	#hibernate configruation
	spring.jpa.hibernate.ddl-auto=update
	spring.jpa.show-sql=true
	spring.jpa.properties.hibernate.format_sql=true
	
#step 8: Repository
* CrudRepository: provide CRUD function
* PagingAndSortingRepository: provides methods to do pagination and sort record
* JpaRepository: Provides JPA related methods such as flushing the presistence context and delete records in a batch.

	Different ways of writing queries in Spring Data JPA
	findByFieldName
	
	
	select * from employees where id in (1,2,3)
	List<Employee> findByIdIn(List<Long> empIds);
	
	@Query("select e from Employee e where e.name=:name and e.salary> :salary")
	List<Employee> findByNameandSalary(@Param("name") String name, @Param String salary);


#setp 9: actuator
	management.endpoints.web.exposure.include=*
	management.endpoint.health.show-details=always
	management.endpoints.web.base-path=/admin
	
	class X implements HealthIndicator{
		
		@Override
		public Health health(){
		  if(condition){
		  	return Health.up().withDetail("DB_Service","").build();
		  }else{
		   	return Health.down().build();
		  }
		}
	} 

#entries in properties files
	

	#spring jpa datasource configuration
	#spring.datasource.driver-class-name=org.h2.Driver
	spring.datasource.driverClassName=org.h2.Driver
	#spring.datasource.url=jdbc:h2:mem:db
	#spring.datasource.url=jdbc:h2:file:~/h2/propertydb
	spring.datasource.url=jdbc:h2:file:./TestDataBase

	spring.datasource.username=sa
	spring.datasource.password=


	#hibernate configruation
	spring.jpa.hibernate.ddl-auto=update
	spring.jpa.show-sql=true
	spring.jpa.properties.hibernate.format_sql=true
	spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.H2Dialect


	#acutator
	#management.endpoint.metrics.enabled=true
	management.endpoints.web.exposure.include=*
	management.endpoint.health.show-details=always
	management.endpoints.web.base-path=/admin
