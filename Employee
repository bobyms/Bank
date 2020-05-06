import java.sql.*;
import java.util.*;
import javafx.scene.control.*;
import oracle.jdbc.driver.OracleDriver;
import javafx.application.Application;
import javafx.event.*;
import javafx.scene.Scene;
import javafx.scene.layout.Pane;
import javafx.stage.Stage;

public class employee extends Application{
    private ArrayList<Integer> branch = new ArrayList<Integer>();
    private ArrayList<Integer> acc = new ArrayList<Integer>();
    private ArrayList<Integer> cus = new ArrayList<Integer>();


    //1. Open Branch methods
    private String get_bnum(){
        //first branch added
        int num = 0;
        String padded = String.format("%03d", num);
        if(branch.size() == 0){
            branch.add(num);
            return padded;
        }
        //If branch 000 was deleted
        else if (branch.size() == 1 && branch.get(0) != 0){
            branch.add(num);
            Collections.sort(branch);
            return padded;
        }
        //2nd branch added
        else if(branch.size() == 1 && branch.get(0) == 0){
            num = 1;
            branch.add(num);
            Collections.sort(branch);
            padded = String.format("%03d", num);
            return padded;
        }
        //Checks for deleted branch numbers and uses them
        else if(branch.size()>0) {
            for (int i = 1; i < branch.size(); i++) {
                if( branch.get(i)-branch.get(i-1) != 1){
                    num = branch.get(i)-1;
                    branch.add(num);
                    Collections.sort(branch);
                    padded = String.format("%03d", num);
                    return padded;
                }
            }
        }
        //Takes highest number after newest branch if no branches before are available
        num = branch.get(branch.size()-1) +1;
        branch.add(num);
        padded = String.format("%03d", num);
        return padded;
    }

    //4
    private String get_cnum(){
        //first customer added
        int num = 0;
        String padded = String.format("%05d", num);
        if(cus.size() == 0){
            cus.add(num);
            return padded;
        }
        //If customer 000 was deleted
        else if (cus.size() == 1 && cus.get(0) != 0){
            cus.add(num);
            Collections.sort(cus);
            return padded;
        }
        //2nd customer added
        else if(cus.size() == 1 && cus.get(0) == 0){
            num = 1;
            cus.add(num);
            Collections.sort(cus);
            padded = String.format("%05d", num);
            return padded;
        }
        //Checks for deleted customer numbers and uses them
        else if(cus.size()>0) {
            for (int i = 1; i < cus.size(); i++) {
                if( cus.get(i)-cus.get(i-1) != 1){
                    num = cus.get(i)-1;
                    cus.add(num);
                    Collections.sort(cus);
                    padded = String.format("%05d", num);
                    return padded;
                }
            }
        }


        //Takes highest number after newest customer if no customers before are available
        num = cus.get(cus.size()-1) +1;
        cus.add(num);
        padded = String.format("%05d", num);
        return padded;
    }
    //3.
    private String get_anum() {

        int num = 0;
        String padded = String.format("%04d", num);
        if (acc.size() == 0) {
            acc.add(num);
            return padded;
        }
        //If account 000 was deleted
        else if (acc.size() == 1 && acc.get(0) != 0) {
            acc.add(num);
            Collections.sort(acc);
            return padded;
        }
        //2nd account added
        else if (acc.size() == 1 && acc.get(0) == 0) {
            num = 1;
            acc.add(num);
            Collections.sort(acc);
            padded = String.format("%04d", num);
            return padded;
        }
        //Checks for deleted account numbers and uses them
        else if (acc.size() > 0) {
            for (int i = 1; i < acc.size(); i++) {
                if (acc.get(i) - acc.get(i - 1) != 1) {
                    num = acc.get(i) - 1;
                    acc.add(num);
                    Collections.sort(acc);
                    padded = String.format("%04d", num);
                    return padded;
                }
            }
        }
        //Takes highest number after newest account if no accounts before are available
        num = acc.get(acc.size()-1) +1;
        acc.add(num);
        padded = String.format("%04d", num);
        return padded;
    }
    //4
    private int get_stat(int money) {
        int stat;
        if (money == 0) stat = 0;
        else if (money > 0 && money < 1000) stat = 1;
        else if (money > 1000 && money < 2000) stat = 2;
        else stat = 3;
        return stat;
    }
    //1
    private String open_branch(String a){
        String x = get_bnum();
        System.out.println("Branch "+x+" has been added");
        Alert alert = new Alert(Alert.AlertType.CONFIRMATION);
        alert.setContentText("Opening Branch: "+ x);
        alert.showAndWait();
        return("insert into branch values ('"+
                x +"','"+a+"')");
    }

    //Close branch methods
    //Checks if number or address is given
    private static boolean isNumeric(String str) {
        try {
            Integer.parseInt(str);
            return true;
        } catch(NumberFormatException e){
            return false;
        }
    }
    //2.Deletes branch with given attribute
    private String close_branch(String x){
        Alert alert = new Alert(Alert.AlertType.CONFIRMATION);
        if (isNumeric(x)) {
            alert.setContentText("Deleted Branch: "+ x);
            alert.showAndWait();
            return ("delete from branch " +
                    "where numb =" + x);
        }
        alert.setContentText("Deleting branches with location: "+x);
        alert.showAndWait();
        return ("delete from branch " +
                "where addy =" + x);
    }

    //3
    private void setup_account(Connection conn) throws SQLException {
        int money = 0;
        TextInputDialog name = new TextInputDialog();
        TextInputDialog bran = new TextInputDialog();
        TextInputDialog amount = new TextInputDialog();
        name.setTitle("Input");
        name.setContentText("Enter Customer name");
        bran.setContentText("Enter branch city or number");
        amount.setContentText("Enter initial amount");
        Optional<String> result = name.showAndWait();
        Optional<String> result2 = bran.showAndWait();
        Optional<String> result3 = amount.showAndWait();
        Statement stmt = conn.createStatement();
        ResultSet rs;
        ResultSet rs2;
        ResultSet rs3;
        Statement stmt1 = conn.createStatement();
        Statement stmt2 = conn.createStatement();

        Alert alert = new Alert(Alert.AlertType.INFORMATION);
        if (result3.isPresent()) money = Integer.parseInt(result3.get());
        if(result.isPresent() && result2.isPresent()){
            try {
                if (isNumeric(result2.get())) {
                    rs2 = stmt1.executeQuery("select numb from branch where numb = '" + result2.get()+"'");
                    rs2.next();
                } else {
                    rs2 = stmt1.executeQuery("select numb from branch where addy = '" + result2.get()+"'");
                    rs2.next();
                }
                rs = stmt.executeQuery("select numb from customer where name = '" + result.get()+"'");
                rs.next();
                String acc_num = get_anum();
                acc_num = rs2.getString(1).concat(acc_num);

                stmt.executeUpdate("insert into account values( '" +
                        acc_num + "' , '" + rs.getString(1) + "' ," + money + ")");
                System.out.println("Account " + acc_num + " added");


            } catch (SQLException e) {
                System.out.println("Info does not exist");
                e.printStackTrace();
            }
        }
        else {
            alert.setContentText("You are missing info");
            alert.showAndWait();
            System.out.println("Nothing created, missing info");
        }
    }



    //9
    private void show_branch(Connection conn, int b) throws SQLException {
        Statement stmt = conn.createStatement();
        int total = 0;
        String x;
        for (Integer a: acc) {
            x=String.valueOf(a);
            x = String.format("%04d", x);
            x=x.substring(0,3);
            if(Integer.parseInt(x) == b){
                ResultSet rs = stmt.executeQuery("select balance from " +
                        "account where numb = '"+String.valueOf(a)+"'");
                System.out.println("Account number :"+a);
                System.out.println("Balance :"+rs.getInt(1));
                rs.next();
                total = total+rs.getInt(1);
            }
        }
        String c = String.format("%03d", b);
        System.out.println("Total in branch "+c+": "+total);
    }

    public void start(Stage primaryStage){
        Pane aPane = new Pane();

        Menu branchs = new Menu("Branch");
        MenuItem open = new MenuItem("Open branch");
        MenuItem close = new MenuItem("Close branch");
        branchs.getItems().addAll(open,close);

        Menu setup = new Menu("Setup");
        MenuItem account = new MenuItem("Setup Account");
        MenuItem setup_customer = new MenuItem("Setup Customer");
        MenuItem close_account = new MenuItem("Close Account");
        setup.getItems().addAll(account,setup_customer,close_account);

        Menu trans = new Menu("Transactions");
        MenuItem withdraw = new MenuItem("Withdraw");
        MenuItem deposit = new MenuItem("Deposit");
        MenuItem transfer = new MenuItem("Transfer");
        trans.getItems().addAll(withdraw,deposit,transfer);

        Menu shows = new Menu("Show");
        MenuItem show_b = new MenuItem("Show Branch");
        MenuItem show_all_branches = new MenuItem("Show All Branches");
        MenuItem show_customer = new MenuItem("Show customer");
        shows.getItems().addAll(show_b,show_all_branches,show_customer);

        try {
            //Connect to server
            DriverManager.registerDriver
                    (new OracleDriver());
            System.out.println("Connecting to JDBC...");

            Connection conn = DriverManager.getConnection
                    ("jdbc:oracle:thin:@localhost:1521:xe","fedora","oracle"); 
            System.out.println("JDBC connected.\n");
            Statement stmt = conn.createStatement();

            //1. Opens new branch
        open.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog add = new TextInputDialog();
                add.setTitle("Input");
                add.setContentText("Enter address for new branch");
                Optional<String> result = add.showAndWait();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);
                if(result.isPresent()){
                    try {
                        stmt.executeUpdate(open_branch(result.get()));
                        alert.setContentText("Branch has been added");
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
                else alert.setContentText("You entered no value");
            }
        });

        //2.Closes existing branch
        close.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog del = new TextInputDialog();
                del.setTitle("Input");
                del.setContentText("Enter address or number of branch to delete");
                Optional<String> result = del.showAndWait();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);
                if(result.isPresent()){
                    try {
                        stmt.executeUpdate(close_branch(result.get()));
                        alert.setContentText("Branch has been deleted");
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
                else alert.setContentText("You entered no value");

            }
        });

        //3
        account.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                try {
                    setup_account(conn);
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        });

        //4
        setup_customer.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog name = new TextInputDialog();
                TextInputDialog bran = new TextInputDialog();
                name.setTitle("Input");
                name.setContentText("Enter Customer name");
                bran.setContentText("Enter branch city or number");
                Optional<String> result = name.showAndWait();
                Optional<String> result2 = bran.showAndWait();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);
                Boolean first = true;

                try {
                    ResultSet rs = stmt.executeQuery("select name from customer where name = '"+ result.get()+"'");
                    rs.next();
                    if(rs.getString(1)!=null) {
                        first = false;
                        alert.setContentText("Customer already setup");
                        alert.showAndWait();}

                } catch (SQLException e) {
                    e.printStackTrace();
                }
                if(first) {
                    int status = 0;
                    try {
                        stmt.executeUpdate("insert into customer values( '" + get_cnum() + "' , '" +
                                result.get() + "' ," + status + ")");
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                    try {
                        setup_account(conn);
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
            }
        });

        //5
        close_account.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog name = new TextInputDialog();
                TextInputDialog bran = new TextInputDialog();
                name.setTitle("Input");
                name.setContentText("Enter Customer name");
                bran.setContentText("Enter branch city or number");
                Optional<String> result = name.showAndWait();
                Optional<String> result2 = bran.showAndWait();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);

                if(result.isPresent()) {
                    try {
                        Statement stmt2 = conn.createStatement();
                        Statement stmt3 = conn.createStatement();
                        ResultSet c_num = stmt.executeQuery("select numb from " +
                                "customer where name = '"+ result.get()+"'");
                        c_num.next();
                        ResultSet bal = stmt2.executeQuery("select balance from " +
                                "account where c_numb = '"+ c_num.getString(1)+"'");
                        ResultSet acc = stmt3.executeQuery("select numb from account where " +
                                "c_numb = '"+ c_num.getString(1)+"'");
                        bal.next();
                        if(bal.getInt(1) < 0){

                            stmt.executeUpdate("delete from account where c_numb = '"+ c_num.getString(1)+"'");
                            System.out.println("Account deleted");
                            if(!acc.next()) {
                                stmt.executeUpdate("delete from customer where numb = '"+ c_num.getString(1)+"'");
                                System.out.println("Customer deleted");
                            }
                        }
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
                else {
                    alert.setContentText("Missing info");
                    alert.showAndWait();
                }
            }
        });

        //6
        withdraw.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog name = new TextInputDialog();
                TextInputDialog acc = new TextInputDialog();
                TextInputDialog money = new TextInputDialog();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);
                name.setContentText("Enter Customer name");
                acc.setContentText("Enter account number");
                money.setContentText("Enter amount to withdraw");
                Optional<String> result = name.showAndWait();
                Optional<String> result2 = acc.showAndWait();
                Optional<String> result3 = money.showAndWait();
                if(result.isPresent() && result2.isPresent() && result3.isPresent()) {
                    try {
                        System.out.println("All fields here");
                        Statement stmt2 = conn.createStatement();
                        Statement stmt3 = conn.createStatement();
                        int x = Integer.parseInt(result3.get());
                        ResultSet rs = stmt.executeQuery("select numb, status from customer where name = '"+
                                result.get()+"'");
                        ResultSet rs2 = stmt2.executeQuery("select c_numb from account where numb = '"+
                                result2.get()+"'");
                        ResultSet rs3 = stmt3.executeQuery("select balance from account where numb = '"+
                                result2.get()+"'");
                        rs.next();
                        rs2.next();
                        rs3.next();
                        System.out.println("All fields here");
                        if(rs.getString(1) == rs2.getString(1)){
                            if(rs3.getInt(1)> x){
                                x = rs3.getInt(1) - x;
                                int stat = get_stat(x);
                                rs3.updateInt(1,x);
                                rs3.updateRow();
                                rs.updateInt(2,stat);
                                rs.updateRow();
                                alert.setContentText("Withdraw made");
                                alert.showAndWait();
                            }
                            else{
                                alert.setContentText("Too broke");
                                alert.showAndWait();
                            }
                        }
                    } catch (SQLException e) {
                        alert.setContentText("Entered info does not match records");
                        alert.showAndWait();
                        e.printStackTrace();
                    }
                }
                else {
                    alert.setContentText("Input missing");
                    alert.showAndWait();
                }
            }
        });

        //7
        deposit.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog name = new TextInputDialog();
                TextInputDialog acc = new TextInputDialog();
                TextInputDialog money = new TextInputDialog();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);
                name.setContentText("Enter Customer name");
                acc.setContentText("Enter account number");
                money.setContentText("Enter amount to deposit");
                Optional<String> result = name.showAndWait();
                Optional<String> result2 = acc.showAndWait();
                Optional<String> result3 = money.showAndWait();
                if(result.isPresent() && result2.isPresent() && result3.isPresent()) {
                    try {
                        Statement stmt2 = conn.createStatement();
                        Statement stmt3 = conn.createStatement();
                        Statement stmt4 = conn.createStatement();
                        int x = Integer.parseInt(result3.get());
                        ResultSet rs = stmt.executeQuery("select numb, status from customer where name = '"+
                                result.get()+"'");
                        rs.next();
                        ResultSet rs2 = stmt2.executeQuery("select c_numb from account where numb = '"+
                                result2.get()+"'");
                        rs2.next();
                        ResultSet rs3 = stmt3.executeQuery("select balance from account where numb = '"+
                                result2.get()+"'");
                        rs3.next();
                        ResultSet rs4 = stmt4.executeQuery("select numb from account where c_numb = '"+
                                rs2.getString(1)+"'");
                        rs4.next();

                        if(rs4.getString(2).isEmpty()){
                            alert.setContentText("No other account to deposit from");
                            alert.showAndWait();
                        }
                        else if(rs.getString(1) == rs2.getString(1)){
                            x = x + rs3.getInt(1);
                            int stat = get_stat(x);
                            rs3.updateInt(1, x);
                            rs3.updateRow();
                            rs.updateInt(2, stat);
                            rs.updateRow();
                            alert.setContentText("Deposit made");
                            alert.showAndWait();
                        }
                    } catch (SQLException e) {
                        alert.setContentText("Entered info does not match records");
                        alert.showAndWait();
                        e.printStackTrace();
                    }
                }
                else {
                    alert.setContentText("Input missing");
                    alert.showAndWait();
                }
            }
        });

        //8
        transfer.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog name = new TextInputDialog();
                TextInputDialog acc = new TextInputDialog();
                TextInputDialog acc2 = new TextInputDialog();
                TextInputDialog money = new TextInputDialog();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);
                name.setContentText("Enter Customer name");
                acc.setContentText("Enter account number to transfer from");
                acc2.setContentText("Enter account number to transfer to");
                money.setContentText("Enter amount to transfer");
                Optional<String> result = name.showAndWait();
                Optional<String> result2 = acc.showAndWait();
                Optional<String> result3 = acc2.showAndWait();
                Optional<String> result4 = money.showAndWait();

                if(result.isPresent() && result2.isPresent() && result3.isPresent() && result4.isPresent()) {
                    try {
                        Statement stmt2 = conn.createStatement();
                        Statement stmt3 = conn.createStatement();
                        Statement stmt4 = conn.createStatement();
                        Statement stmt5 = conn.createStatement();
                        int x = Integer.parseInt(result4.get());
                        ResultSet rs = stmt.executeQuery("select numb, status from customer where name = '" +
                                result.get()+"'");
                        ResultSet rs2 = stmt2.executeQuery("select c_numb from account where numb = '"+
                                result2.get()+"'");
                        ResultSet rs3 = stmt3.executeQuery("select balance from account where numb = '"+
                                result2.get()+"'");
                        ResultSet rs4 = stmt4.executeQuery("select balance from account where numb = '"+
                                result3.get()+"'");
                        ResultSet rs5 = stmt5.executeQuery("select c.status from customer c natural join " +
                                "account a where a.numb = '"+ result3.get()+"'");
                        rs.next();
                        rs2.next();
                        rs3.next();
                        rs4.next();
                        rs5.next();
                        if(rs.getString(1) == rs2.getString(1)){
                            if(rs3.getInt(1)> x){
                                x = rs3.getInt(1) - x;
                                int y = rs4.getInt(1) + x;
                                int stat = get_stat(x);
                                int stat2= get_stat(y);
                                rs3.updateInt(1,x);
                                rs3.updateRow();
                                rs.updateInt(2,stat);
                                rs.updateRow();
                                rs4.updateInt(1,y);
                                rs4.updateRow();
                                rs5.updateInt(1,stat2);
                                rs5.updateRow();
                                alert.setContentText("Transfer made");
                                alert.showAndWait();
                            }
                            else{
                                alert.setContentText("Too broke");
                                alert.showAndWait();
                            }
                        }
                    } catch (SQLException e) {
                        alert.setContentText("Entered info does not match records");
                        alert.showAndWait();
                        e.printStackTrace();
                    }
                }
                else {
                    alert.setContentText("Input missing");
                    alert.showAndWait();
                }
            }
        });

        //9
        show_b.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog bran = new TextInputDialog();
                bran.setContentText("Enter Branch info");
                Optional<String> result = bran.showAndWait();
                if(result.isPresent()) {
                    try {
                        show_branch(conn, Integer.parseInt(result.get()));
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
            }
        });

        //10
        show_all_branches.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                for (int b: branch) {
                    try {
                        show_branch(conn, b);
                    } catch (SQLException e) {
                        e.printStackTrace();
                    }
                }
            }
        });

        //11
        show_customer.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                TextInputDialog name = new TextInputDialog();
                name.setTitle("Input");
                name.setContentText("Enter customer name");
                Optional<String> result = name.showAndWait();
                Alert alert = new Alert(Alert.AlertType.INFORMATION);
                ResultSet rs;
                ResultSet rs2;
                ResultSet rs3;

                int total=0;
                if(result.isPresent()){
                    try {
                        Statement stmt2 = conn.createStatement();
                        Statement stmt3 = conn.createStatement();

                        rs = stmt.executeQuery("select numb from customer where name = '"+result.get()+"'");
                        rs.next();
                        rs2 = stmt2.executeQuery("select numb, status from customer " +
                                "where name = '" + result.get()+"'");

                        rs3 = stmt3.executeQuery("select numb, balance from account " +
                                "where c_numb = '" + rs.getString(1)+"'");

                        while (rs2.next()){
                            System.out.println("Customer Number: "+ rs2.getString("numb"));
                            System.out.println("Status: "+ rs2.getString("status"));
                        }
                        while (rs3.next()){
                            System.out.println("Account Number: "+rs3.getString("numb"));
                            System.out.println("Balance: "+rs3.getInt("balance"));
                            total = total + rs3.getInt("balance");
                        }
                        //int stat = get_stat(total);
                        //rs2.updateInt(1,stat);
                        //rs2.updateRow();

                        System.out.println("Total in all accounts for customer "+result.get()+": "+total);
                    } catch (SQLException e) {
                        alert.setContentText("Customer does not exist");
                        e.printStackTrace();
                    }
                }
                else alert.setContentText("You entered no value");
            }
        });
        //stmt.close();
        //conn.close();
        }

        catch(Exception e)
        {
            System.out.println("SQL exception: ");
            e.printStackTrace();
            System.exit(-1);
        }
        MenuBar menuBar = new MenuBar();
        aPane.getChildren().addAll(menuBar);
        menuBar.getMenus().addAll(branchs,setup,trans,shows);
        primaryStage.setTitle("JDBC Bank");
        primaryStage.setScene(new Scene(aPane, 250,200));
        primaryStage.show();
    }
    public static void main(String[] args) {
        launch(args);

    }
}
