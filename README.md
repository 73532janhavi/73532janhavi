- 👋 Hi, I’m @73532janhavi
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
73532janhavi/73532janhavi is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
using Microsoft.Data.SqlClient;
using System.Data;
using WebApplication2.Models;

namespace WebApplication2.Models
{
    public class Employee
    {
        public int EmpNo { get; set; }

        public string Name { get; set; }

        public decimal Basic {  get; set; }

        public int DeptNo { get; set; }

        

        internal static List<Employee> GetAllEmployees()
        { 
                List<Employee> lstEmps = new List<Employee>();

                SqlConnection cn = new SqlConnection();
                cn.ConnectionString = @"Data Source=(LocalDb)\MsSqlLocalDb;Initial Catalog=Employees;Integrated Security=True";
                try
                {
                    cn.Open();
                    SqlCommand cmd = new SqlCommand();
                    cmd.Connection = cn;
                    cmd.CommandType = System.Data.CommandType.Text;
                    cmd.CommandText = "select * from Employees";

                    SqlDataReader dr = cmd.ExecuteReader();
                    while (dr.Read())
                    {
                        Employee obj = new Employee();
                        obj.EmpNo = dr.GetInt32("EmpNo");
                        obj.Name = dr.GetString("Name");
                        obj.Basic = dr.GetDecimal("Basic");
                        obj.DeptNo = dr.GetInt32("DeptNo");
                        lstEmps.Add(obj);

                        //lstEmps.Add(new Employee { EmpNo = dr.GetInt32("EmpNo") })
                    }
                    dr.Close();

                }
                catch (Exception)
                {
                    throw;
                }
                finally
                {
                    cn.Close();
                }
                //
                return lstEmps;
            }

        internal static Employee GetSingleEmployee(int id)
        {
            
                Employee obj = new Employee();
                //
                SqlConnection cn = new SqlConnection();
                cn.ConnectionString = @"Data Source=(LocalDb)\MsSqlLocalDb;Initial Catalog=Employees;Integrated Security=True";
                try
                {
                    cn.Open();
                    SqlCommand cmd = new SqlCommand();
                    cmd.Connection = cn;
                    cmd.CommandType = System.Data.CommandType.Text;
                    cmd.CommandText = "select * from Employees where EmpNo=@EmpNo";
                    cmd.Parameters.AddWithValue("@EmpNo", id);

                    SqlDataReader dr = cmd.ExecuteReader();
                    //dr.HasRows
                    if (dr.Read())
                    {
                        obj.EmpNo = dr.GetInt32("EmpNo");
                        obj.Name = dr.GetString("Name");
                        obj.Basic = dr.GetDecimal("Basic");
                        obj.DeptNo = dr.GetInt32("DeptNo");

                    }
                    else
                        obj = null;
                    dr.Close();

                }
                catch (Exception)
                {
                    throw;
                }
                finally
                {
                    cn.Close();
                }
                
                return obj;
        }

        internal static Employee UpdateEmployee(int id,Employee obj)
        {
            //Employee obj = new Employee();
            SqlConnection cn = new SqlConnection();
            //Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=YcpOct23;Integrated Security=True;Connect Timeout=30;Encrypt=False;Trust Server Certificate=False;Application Intent=ReadWrite;Multi Subnet Failover=False
            cn.ConnectionString = @"Data Source=(LocalDb)\MSSQLLocalDB;Initial Catalog=Employees;Integrated Security=True";
            try
            {
                cn.Open();
                SqlCommand cmd = new SqlCommand();
                cmd.Connection = cn;

                cmd.CommandType = System.Data.CommandType.Text;

                cmd.CommandText = "Update Employees Set Name=@Name , Basic = @Basic , DeptNo=@DeptNo where EmpNo=@EmpNo";

                cmd.Parameters.AddWithValue("@Name", obj.Name);
                cmd.Parameters.AddWithValue("@Basic",obj.Basic);
                cmd.Parameters.AddWithValue("@DeptNo", obj.DeptNo);
                cmd.Parameters.AddWithValue("@EmpNo", obj.EmpNo);

                cmd.ExecuteNonQuery();

                Console.WriteLine("Successful");
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
            finally
            {
                cn.Close();
            }
            return obj;
        }
        internal static Employee DeleteEmployee(int id)
        {
            Employee obj = new Employee();
            SqlConnection cn = new SqlConnection();
            //Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=YcpOct23;Integrated Security=True;Connect Timeout=30;Encrypt=False;Trust Server Certificate=False;Application Intent=ReadWrite;Multi Subnet Failover=False
            cn.ConnectionString = @"Data Source=(LocalDb)\MSSQLLocalDB;Initial Catalog=Employees;Integrated Security=True";
            try
            {
                cn.Open();
                SqlCommand cmd = new SqlCommand();
                cmd.Connection = cn;

                cmd.CommandType = System.Data.CommandType.Text;

                cmd.CommandText = $"Delete Employees where EmpNo=@EmpNo";

                cmd.Parameters.AddWithValue("@EmpNo", id);

                cmd.ExecuteNonQuery();

                Console.WriteLine("Successful");
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
            finally
            {
                cn.Close();
            }
            return obj;
        }

        internal static Employee InsertEmployee(Employee obj)
        {
            SqlConnection cn = new SqlConnection();
            //Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=YcpOct23;Integrated Security=True;Connect Timeout=30;Encrypt=False;Trust Server Certificate=False;Application Intent=ReadWrite;Multi Subnet Failover=False
            cn.ConnectionString = @"Data Source=(LocalDb)\MSSQLLocalDB;Initial Catalog=Employees;Integrated Security=True";
            try
            {
                cn.Open();
                SqlCommand cmd = new SqlCommand();
                cmd.Connection = cn;

                cmd.CommandType = System.Data.CommandType.Text;

                cmd.CommandText = "Insert into Employees values(@EmpNo , @Name ,@Basic ,@DeptNo)";
                cmd.Parameters.AddWithValue("@EmpNo", obj.EmpNo);
                cmd.Parameters.AddWithValue("@Name", obj.Name);
                cmd.Parameters.AddWithValue("@Basic", obj.Basic);
                cmd.Parameters.AddWithValue("@DeptNo", obj.DeptNo);

                cmd.ExecuteNonQuery();

                Console.WriteLine("Successful");
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
            finally
            {
                cn.Close();
            }
            return obj;
        }
    }
}
