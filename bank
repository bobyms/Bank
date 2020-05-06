import java.sql.*;

public class bank {
    public static void main(String[] args) {
        try {
            //Connect to server
            DriverManager.registerDriver
                    (new oracle.jdbc.driver.OracleDriver());
            System.out.println("Connecting to JDBC...");

            Connection conn = DriverManager.getConnection
                    ("jdbc:oracle:thin:@localhost:1521:xe","fedora","oracle")
            System.out.println("JDBC connected.\n");

            //Create tables
            Statement stmt = conn.createStatement();
            stmt.execute("create table branch( "+
                    "numb varchar(3) NOT NULL Primary Key, "+
                    "addy varchar(10) NOT NULL)");

            stmt.execute("create table customer( "+
                    "numb varchar(5) NOT NULL Primary Key, "+
                    "name varchar(10) NOT NULL unique, "+
                    "status int NOT NULL)");

            stmt.execute("create table account( "+
                    "numb varchar(7) NOT NULL Primary Key, "+
                    "c_numb varchar(5) NOT NULL,"+
                    "balance int NOT NULL,"+
                    "foreign key (c_numb) references customer(numb) ON DELETE CASCADE)");

            System.out.println("Tables created.");
            stmt.close();
            conn.close();
        }
        catch(Exception e)
        {
            System.out.println("SQL exception: ");
            e.printStackTrace();
            System.exit(-1);
        }
    }
}
