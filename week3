package com.klu;

import java.util.List;
import org.hibernate.Session;
import org.hibernate.query.Query;

public class HQLDemo {

 public static void main(String[] args) {

  Session session = HibernateUtil.getSessionFactory().openSession();

  /* 1. Retrieve all products sorted by price (Ascending) */
  Query<Product> q1 = session.createQuery(
    "from Product p order by p.price asc", Product.class);
  List<Product> ascList = q1.list();
  System.out.println("Price Ascending:");
  for(Product p : ascList) {
   System.out.println(p.getName() + " " + p.getPrice());
  }

  /* 2. Retrieve all products sorted by price (Descending) */
  Query<Product> q2 = session.createQuery(
    "from Product p order by p.price desc", Product.class);
  List<Product> descList = q2.list();
  System.out.println("\nPrice Descending:");
  for(Product p : descList) {
   System.out.println(p.getName() + " " + p.getPrice());
  }

  /* 3. Sort products by quantity (highest first) */
  Query<Product> q3 = session.createQuery(
    "from Product p order by p.quantity desc", Product.class);
  System.out.println("\nQuantity Highest First:");
  for(Product p : q3.list()) {
   System.out.println(p.getName() + " " + p.getQuantity());
  }

  /* 4. Pagination – First 3 products */
  Query<Product> q4 = session.createQuery("from Product", Product.class);
  q4.setFirstResult(0);
  q4.setMaxResults(3);
  System.out.println("\nFirst 3 Products:");
  for(Product p : q4.list()) {
   System.out.println(p.getName());
  }

  /* 5. Pagination – Next 3 products */
  Query<Product> q5 = session.createQuery("from Product", Product.class);
  q5.setFirstResult(3);
  q5.setMaxResults(3);
  System.out.println("\nNext 3 Products:");
  for(Product p : q5.list()) {
   System.out.println(p.getName());
  }

  /* 6a. Count total number of products */
  Query<Long> q6 = session.createQuery(
    "select count(p) from Product p", Long.class);
  System.out.println("\nTotal Products: " + q6.uniqueResult());

  /* 6b. Count products where quantity > 0 */
  Query<Long> q7 = session.createQuery(
    "select count(p) from Product p where p.quantity > 0", Long.class);
  System.out.println("Products with quantity > 0: " + q7.uniqueResult());

  /* 6c. Count products grouped by description */
  Query<Object[]> q8 = session.createQuery(
    "select p.description, count(p) from Product p group by p.description");
  System.out.println("\nCount Grouped by Description:");
  for(Object[] row : q8.list()) {
   System.out.println(row[0] + " : " + row[1]);
  }

  /* 6d. Minimum and Maximum price */
  Query<Object[]> q9 = session.createQuery(
    "select min(p.price), max(p.price) from Product p");
  Object[] result = q9.uniqueResult();
  System.out.println("\nMin Price: " + result[0]);
  System.out.println("Max Price: " + result[1]);

  /* 7. GROUP BY description */
  Query<Object[]> q10 = session.createQuery(
    "select p.description, sum(p.quantity) from Product p group by p.description");
  System.out.println("\nGroup By Description (Quantity Sum):");
  for(Object[] row : q10.list()) {
   System.out.println(row[0] + " : " + row[1]);
  }

  /* 8. WHERE clause – price range */
  Query<Product> q11 = session.createQuery(
    "from Product p where p.price between 500 and 5000", Product.class);
  System.out.println("\nProducts in Price Range 500–5000:");
  for(Product p : q11.list()) {
   System.out.println(p.getName() + " " + p.getPrice());
  }

  /* 9a. LIKE – names starting with 'L' */
  Query<Product> q12 = session.createQuery(
    "from Product p where p.name like 'L%'", Product.class);
  System.out.println("\nNames starting with L:");
  for(Product p : q12.list()) {
   System.out.println(p.getName());
  }

  /* 9b. LIKE – names ending with 'r' */
  Query<Product> q13 = session.createQuery(
    "from Product p where p.name like '%r'", Product.class);
  System.out.println("\nNames ending with r:");
  for(Product p : q13.list()) {
   System.out.println(p.getName());
  }

  /* 9c. LIKE – names containing 'a' */
  Query<Product> q14 = session.createQuery(
    "from Product p where p.name like '%a%'", Product.class);
  System.out.println("\nNames containing 'a':");
  for(Product p : q14.list()) {
   System.out.println(p.getName());
  }

  /* 9d. Names with exact character length (5) */
  Query<Product> q15 = session.createQuery(
    "from Product p where length(p.name) = 5", Product.class);
  System.out.println("\nNames with length 5:");
  for(Product p : q15.list()) {
   System.out.println(p.getName());
  }

  session.close();
 }
}
