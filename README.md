# HibernateSecondLevelCache
HibernateSecondLevelCache

how to run:

    create a schema hibernateCache in mysql
    add project to tomcat and start.
    student table will create automatically in hibernateCache.
    insert a record with id 1.
    execute below url 2 times: 
    http://localhost:8080/HibernateCache/getStudent

output on console:

*********** session1*******
Hibernate: select student0_.ID as ID1_0_0_, student0_.STUDENT_NAME as STUDENT_2_0_0_ from STUDENT student0_ where student0_.ID=?

first query result student is::Student [id=1, studentName=sushil]
*********** session2*******
second query result student is::Student [id=1, studentName=sushil]



*********** session1*******
first query result student is::Student [id=1, studentName=sushil]
*********** session2*******
second query result student is::Student [id=1, studentName=sushil]

As you see in below code of call StudentDaoImpl, i tried to get same record of student with same id so hibernate second cache  work at here, you can see above output the query execute single time in different session and we get same output.
#query execute only first time .

       System.out.println("*********** session1*******");
			 Session session1=sessionFactory.openSession();
			 Student stud = session1.get(Student.class, id);
			 System.out.println("first query result student is::"+stud);
			 session1.close();
			 
			 System.out.println("*********** session2*******");
			 Session session2=sessionFactory.openSession();
			 Student stud2 = session2.get(Student.class, id);
			 System.out.println("second query result student is::"+stud2);
			 session2.close();
			 
