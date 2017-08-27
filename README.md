using System;
using System.Collections.Generic;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;

public partial class _Default : System.Web.UI.Page
{
    String ConnectionString = "Database=STICO;Server=DESKTOP-QHNNGVF;Integrated Security=True;connect timeout = 60";
    DataSet ds = new DataSet();
    DataTable dt = new DataTable();
    protected void Page_Load(object sender, EventArgs e)
    {
        try
        {

            int Year = DateTime.Today.Year;
            txtCurrentAccountYear.Text = Convert.ToString(Year + "-" + (Year + 1));
            int Month = DateTime.Today.Month;
            DateTime time;
            string format = "";
            SqlConnection myConnection = new SqlConnection(ConnectionString);
            myConnection.Open();
            SqlCommand cmd = new SqlCommand("Select Report_No,Name_Of_Sample,Byers_Name,Date_Of_Received,Sample_Received_From from Master_STICOO", myConnection);
            SqlDataAdapter da = new SqlDataAdapter(cmd);
            da.Fill(ds);
            dt = ds.Tables[0];
            if (dt.Rows.Count > 0)
            {
                gvReportDisplay.DataSource = dt;
                if (!IsPostBack)
                {
                    gvReportDisplay.DataBind();
                    txtReportDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
                   txtDateOfReceived.Text = DateTime.Now.ToString("MM-dd-yyyy");
                    txtDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
                }
                else { }
                txtReportDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
               // txtDateOfReceived.Text = DateTime.Now.ToString("MM-dd-yyyy");
                txtDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
            }
            else
            {




                txtReportDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
             //   txtDateOfReceived.Text = DateTime.Now.ToString("MM-dd-yyyy");
                txtDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
                if (!IsPostBack)
                {
                    gvReportDisplay.DataBind();
                    txtDateOfReceived.Text = DateTime.Now.ToString("MM-dd-yyyy");
                }
                else { }
            }
        }
        catch (Exception ex)
        {
            lblresult.Text = Convert.ToString(ex);
        }
    }
    protected void btnSave_Click(object sender, EventArgs e)
    {
        if (!string.IsNullOrEmpty(txtDateOfReceived.Text))
        {
            string DateOfReceived = txtDateOfReceived.Text;
            string[] ValidationCurrentYear = DateOfReceived.Split('-');
            string Month = ValidationCurrentYear[0];
            string Date = ValidationCurrentYear[1];
            string year = ValidationCurrentYear[2];
            int monthI = Convert.ToInt32(Month);
            int YearI = Convert.ToInt32(year);
            int Year1 = YearI + 1;
            int Year0 = YearI - 1;
            if (ddlSelectAccountYear.SelectedItem.Text == year + "-" + Year1 || ddlSelectAccountYear.SelectedItem.Text == Year0 + "-" + year)
            {
                try
                {
                    SqlConnection myConnection1 = new SqlConnection(ConnectionString);
                    myConnection1.Open();
                    DateTime Report_Date = Convert.ToDateTime(txtReportDate.Text); //DateTime.Now;
                    String Accounting_Year = txtCurrentAccountYear.Text;
                    String Current_Year = ddlSelectAccountYear.SelectedItem.Text;
                    String Sample_Received_From = txtSampleReceivedFrom.Text;
                    String Name_Of_Sample = txtNameOfSample.Text;
                    String Byers_Name = txtBuyersName.Text;
                    DateTime Date_Of_Received = Convert.ToDateTime(txtDateOfReceived.Text);
                    String Bug = txtBugs.Text;
                    String Lot_No = txtLotNo.Text;
                    String Track_No = txtLotNo.Text;
                    DateTime Tracking_Date = DateTime.Now;
                    String Seal_Impression = txtSealImpression.Text;
                    String Element1 = txtElement1.Text;
                    String Element2 = txtElement2.Text;
                    String Element3 = txtElement3.Text;
                    String Element4 = txtElement4.Text;
                    String Element5 = txtElement5.Text;
                    String Element6 = txtElement6.Text;
                    String Element7 = txtElement7.Text;
                    String Element8 = txtElement8.Text;
                    String Element9 = txtElement9.Text;
                    String Element10 = txtElement10.Text;
                    String Element1_Percentage = txtPercentage1.Text;
                    String Element2_Percentage = txtPercentage2.Text;
                    String Element3_Percentage = txtPercentage3.Text;
                    String Element4_Percentage = txtPercentage4.Text;
                    String Element5_Percentage = txtPercentage5.Text;
                    String Element6_Percentage = txtPercentage6.Text;
                    String Element7_Percentage = txtPercentage7.Text;
                    String Element8_Percentage = txtPercentage8.Text;
                    String Element9_Percentage = txtPercentage9.Text;
                    String Element10_Percentage = txtPercentage10.Text;
                    SqlCommand cmd1 = new SqlCommand();
                    if (ddlReportType.SelectedValue == "New")
                    {
                        String Report_No = txtReportNo.Text;
                        cmd1 = new SqlCommand("insert into Master_STICOO(Report_No,Report_Date,Accounting_Year,Current_Year,Sample_Received_From,Name_Of_Sample,Byers_Name,Date_Of_Received,Bug,Lot_No,Track_No,Tracking_Date,Seal_Impression,Element1,Element2,Element3,Element4,Element5,Element7,Element8,Element10,Element1_Percentage,Element2_Percentage,Element3_Percentage,Element4_Percentage,Element5_Percentage,Element7_Percentage,Element8_Percentage,Element9_Percentage,Element10_Percentage,Element9,Element6_Percentage,Element6) values('" + Report_No + "','" + Report_Date + "','" + Accounting_Year + "','" + Current_Year + "','" + Sample_Received_From + "','" + Name_Of_Sample + "','" + Byers_Name + "','" + Date_Of_Received + "','" + Bug + "','" + Lot_No + "','" + Track_No + "','" + Tracking_Date + "','" + Seal_Impression + "','" + Element1 + "','" + Element2 + "','" + Element3 + "','" + Element4 + "','" + Element5 + "','" + Element7 + "','" + Element8 + "','" + Element10 + "','" + Element1_Percentage + "','" + Element2_Percentage + "','" + Element3_Percentage + "','" + Element4_Percentage + "','" + Element5_Percentage + "','" + Element7_Percentage + "','" + Element8_Percentage + "','" + Element9_Percentage + "','" + Element10_Percentage + "','" + Element9 + "','" + Element6_Percentage + "','" + Element6 + "')", myConnection1);
                    }
                    else if (ddlReportType.SelectedValue == "Urgent")
                    {
                        String Report_No = txtReportNo.Text;
                        cmd1 = new SqlCommand("insert into Master_STICOO1UR(Report_No,Report_Date,Accounting_Year,Current_Year,Sample_Received_From,Name_Of_Sample,Byers_Name,Date_Of_Received,Bug,Lot_No,Track_No,Tracking_Date,Seal_Impression,Element1,Element2,Element3,Element4,Element5,Element7,Element8,Element10,Element1_Percentage,Element2_Percentage,Element3_Percentage,Element4_Percentage,Element5_Percentage,Element7_Percentage,Element8_Percentage,Element9_Percentage,Element10_Percentage,Element9,Element6_Percentage,Element6) values('" + Report_No + "','" + Report_Date + "','" + Accounting_Year + "','" + Current_Year + "','" + Sample_Received_From + "','" + Name_Of_Sample + "','" + Byers_Name + "','" + Date_Of_Received + "','" + Bug + "','" + Lot_No + "','" + Track_No + "','" + Tracking_Date + "','" + Seal_Impression + "','" + Element1 + "','" + Element2 + "','" + Element3 + "','" + Element4 + "','" + Element5 + "','" + Element7 + "','" + Element8 + "','" + Element10 + "','" + Element1_Percentage + "','" + Element2_Percentage + "','" + Element3_Percentage + "','" + Element4_Percentage + "','" + Element5_Percentage + "','" + Element7_Percentage + "','" + Element8_Percentage + "','" + Element9_Percentage + "','" + Element10_Percentage + "','" + Element9 + "','" + Element6_Percentage + "','" + Element6 + "')", myConnection1);
                    }
                    else if (ddlReportType.SelectedValue == "SubReport")
                    {
                        String Report_No = ddlSubReport.SelectedValue;
                        String SubReportNumber = txtReportNo.Text;
                        cmd1 = new SqlCommand("insert into Master_STICOO2SUB(Report_No,Report_Date,Accounting_Year,Current_Year,Sample_Received_From,Name_Of_Sample,Byers_Name,Date_Of_Received,Bug,Lot_No,Track_No,Tracking_Date,Seal_Impression,Element1,Element2,Element3,Element4,Element5,Element7,Element8,Element10,Element1_Percentage,Element2_Percentage,Element3_Percentage,Element4_Percentage,Element5_Percentage,Element7_Percentage,Element8_Percentage,Element9_Percentage,Element10_Percentage,Element9,Element6_Percentage,Element6,SubReportNumber) values('" + Report_No + "','" + Report_Date + "','" + Accounting_Year + "','" + Current_Year + "','" + Sample_Received_From + "','" + Name_Of_Sample + "','" + Byers_Name + "','" + Date_Of_Received + "','" + Bug + "','" + Lot_No + "','" + Track_No + "','" + Tracking_Date + "','" + Seal_Impression + "','" + Element1 + "','" + Element2 + "','" + Element3 + "','" + Element4 + "','" + Element5 + "','" + Element7 + "','" + Element8 + "','" + Element10 + "','" + Element1_Percentage + "','" + Element2_Percentage + "','" + Element3_Percentage + "','" + Element4_Percentage + "','" + Element5_Percentage + "','" + Element7_Percentage + "','" + Element8_Percentage + "','" + Element9_Percentage + "','" + Element10_Percentage + "','" + Element9 + "','" + Element6_Percentage + "','" + Element6 + "','" + SubReportNumber + "')", myConnection1);
                    }
                    else { }
                    int result = cmd1.ExecuteNonQuery();
                    if (result >= 1)
                    {
                        btnSave.Enabled = false;
                        lblresult.Text = "Record save Successfully";
                        txtReportNo.Text = "";
                        txtReportDate.Text = "";
                        txtCurrentAccountYear.Text = "";
                        ddlSelectAccountYear.SelectedItem.Text = "";
                        txtSampleReceivedFrom.Text = "";
                        txtNameOfSample.Text = "";
                        txtBuyersName.Text = "";
                        txtDateOfReceived.Text = "";
                        txtBugs.Text = "";
                        txtLotNo.Text = "";
                        txtLotNo.Text = "";
                        txtDate.Text = "";
                        txtWagonNo.Text = "";
                        txtSealImpression.Text = "";
                        txtElement1.Text = "";
                        txtElement2.Text = "";
                        txtElement3.Text = "";
                        txtElement4.Text = "";
                        txtElement5.Text = "";
                        txtElement6.Text = "";
                        txtElement7.Text = "";
                        txtElement8.Text = "";
                        txtElement9.Text = "";
                        txtElement10.Text = "";
                        txtPercentage1.Text = "";
                        txtPercentage2.Text = "";
                        txtPercentage3.Text = "";
                        txtPercentage4.Text = "";
                        txtPercentage5.Text = "";
                        txtPercentage6.Text = "";
                        txtPercentage7.Text = "";
                        txtPercentage8.Text = "";
                        txtPercentage9.Text = "";
                        txtPercentage10.Text = "";

                    }
                    gvReportDisplay.DataBind();
                    Response.AppendHeader("Refresh", "120");
                }
                catch (Exception ex)
                {
                    lblresult.Text = Convert.ToString(ex);
                }


            }
            else
            {
                lblresult.Text = "Select accounting year does not match!!";
            }
        }
        else
        {
            lblresult.Text = "Date of received is blank!!";
        }

    }
    protected void btnErase_Click(object sender, EventArgs e)
    {
        foreach (GridViewRow row in gvReportDisplay.Rows)
        {
            SqlConnection myConnection = new SqlConnection(ConnectionString);
            myConnection.Open();
            CheckBox chkb = (CheckBox)row.FindControl("ChkSelect");
            if (chkb != null && chkb.Checked)
            {
                string Value = Convert.ToString(gvReportDisplay.Rows[0].Cells[1].Text);
                string query = "delete from Master_STIC where Report_No='" + Value + "'";
                SqlCommand cmd = new SqlCommand(query, myConnection);
                cmd.ExecuteNonQuery();
            }
            gvReportDisplay.DataBind();
        }
        Response.AppendHeader("Refresh", "120");
    }

    protected void btnPrintR_Click(object sender, EventArgs e)
    {      
        //    Response.Redirect("/ReportPrint.aspx?ReportStartDate=" + ddlStartingDate.SelectedValue + " &ReportEndDate=" + ddlEndingDate.SelectedValue);       
    }
    protected void btnbtnRefresh_Click(object sender, EventArgs e)
    {
        Response.AppendHeader("Refresh", "120");
        btnSave.Enabled = true;
    }
    protected void DropDownList1_SelectedIndexChanged(object sender, EventArgs e)
    {
        if (!string.IsNullOrEmpty(txtDateOfReceived.Text))
        {
            string DateOfReceived = txtDateOfReceived.Text;
            string[] ValidationCurrentYear = DateOfReceived.Split('-');
            string Month = ValidationCurrentYear[0];
            string Date = ValidationCurrentYear[1];
            string year = ValidationCurrentYear[2];
            int monthI = Convert.ToInt32(Month);
            int YearI = Convert.ToInt32(year);
            int Year1 = YearI + 1;
            int Year0 = YearI - 1;
            
            if (monthI > 3)
            {
                if (!IsPostBack)
                {
                    ddlSelectAccountYear.SelectedIndex = -1;
                    ddlSelectAccountYear.DataBind();
                    ddlSelectAccountYear.Items.Insert(0, new ListItem(year + "-" + Year1, "0"));
                }
            }
            else
            {
                if (!IsPostBack)
                {
                    ddlSelectAccountYear.SelectedIndex = -1;
                    ddlSelectAccountYear.DataBind();
                    ddlSelectAccountYear.Items.Insert(0, new ListItem(Year0 + "-" + year, "0"));
                }
            }
        }
        else
        {
        }
        txtReportNo.Text = "";
        if (ddlReportType.SelectedValue == "New")
        {
            txtReportDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
            if (!IsPostBack) { txtDateOfReceived.Text = DateTime.Now.ToString("MM-dd-yyyy"); }
            else { }
           
            txtDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
            SqlConnection myConnection = new SqlConnection(ConnectionString);
            myConnection.Open();
            SqlCommand cmd = new SqlCommand("Select Report_No,Name_Of_Sample,Byers_Name,Date_Of_Received,Sample_Received_From from Master_STICOO", myConnection);
            SqlDataAdapter da = new SqlDataAdapter(cmd);
            DataSet ds1 = new DataSet();
            da.Fill(ds1);
            dt = ds1.Tables[0];
            if (dt.Rows.Count >= 1)
            {
                int Count = dt.Rows.Count;
                string FCount = string.Empty;
                if (Count >= 1 && Count < 10)
                {
                    FCount = Convert.ToString("000" + Count);
                }
                if (Count >= 10 && Count < 100)
                {
                    FCount = Convert.ToString("00" + Count);
                }
                else if (Count >= 100 && Count < 1000)
                {
                    FCount = Convert.ToString("0" + Count);
                }
                else if (Count >= 1000 && Count < 10000)
                {
                    FCount = Convert.ToString(Count);
                }
                else if (Count >= 10000 && Count < 100000)
                {
                    FCount = Convert.ToString(Count);
                }
                else if (Count >= 100000)
                {
                    FCount = Convert.ToString(Count);
                }
                else
                {
                    //FCount = Convert.ToString("0000" + Count);
                }
                if (System.DateTime.Now.Month > 10)
                {
                    txtReportNo.Text = "N/" + System.DateTime.Now.Month + "/" + FCount;

                }
                else
                {
                    txtReportNo.Text = "N/" + "0" + System.DateTime.Now.Month + "/" + FCount;
                }
            }
            else
            {
                if (System.DateTime.Now.Month > 10)
                {
                    txtReportNo.Text = "N/" + System.DateTime.Now.Month + "/0000";
                }
                else
                {
                    txtReportNo.Text = "N/" + "0" + System.DateTime.Now.Month + "/0000";
                }
            }
        }
        else if (ddlReportType.SelectedValue == "Urgent")
        {
            txtReportDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
            if (!IsPostBack)
            {
                txtDateOfReceived.Text = DateTime.Now.ToString("MM-dd-yyyy");
            }
            else { }
            txtDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
           
            if (System.DateTime.Now.Month > 10)
            {
                txtReportNo.Text = "U/" + System.DateTime.Now.Month + "/";
            }
            else
            {
                txtReportNo.Text = "U/" + "0" + System.DateTime.Now.Month + "/";
            }           
        }
        else if (ddlReportType.SelectedValue == "SubReport")
        {

            SqlConnection myConnection = new SqlConnection(ConnectionString);
            myConnection.Open();
            SqlCommand cmd = new SqlCommand("Select * from Master_STICOO", myConnection);
            SqlDataAdapter da = new SqlDataAdapter(cmd);
            da.Fill(ds);
            dt = ds.Tables[0];
            ddlSubReport.DataSource = dt;
            ddlSubReport.DataTextField = "Report_No";
            ddlSubReport.DataValueField = "Report_No";
            ddlSubReport.DataBind();
        }
        else
        {
        }
    }
    protected void ddlSubReport_SelectedIndexChanged(object sender, EventArgs e)
    {
        txtReportDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
        if (!IsPostBack)
        {
            txtDateOfReceived.Text = DateTime.Now.ToString("MM-dd-yyyy");
        }
        else { }
        txtDate.Text = DateTime.Now.ToString("MM-dd-yyyy");
        DataSet ds1 = new DataSet();
        SqlConnection myConnection1 = new SqlConnection(ConnectionString);
        myConnection1.Open();
        SqlCommand cmd1 = new SqlCommand("Select * from Master_STICOO2SUB where Report_No='" + ddlSubReport.SelectedValue + "'", myConnection1);
        SqlDataAdapter da1 = new SqlDataAdapter(cmd1);
        da1.Fill(ds1);
        DataTable dt1 = new DataTable();
        dt1 = ds1.Tables[0];
        if (dt1.Rows.Count > 0)
        {
            if (dt1.Rows.Count == 1)
            {
                txtReportNo.Text = ddlSubReport.SelectedValue + "/B";
            }
            else if (dt1.Rows.Count == 2)
            {
                txtReportNo.Text = ddlSubReport.SelectedValue + "/C";
            }
            else if (dt1.Rows.Count == 3)
            {
                txtReportNo.Text = ddlSubReport.SelectedValue + "/D";
            }
            else if (dt1.Rows.Count == 4)
            {
                txtReportNo.Text = ddlSubReport.SelectedValue + "/E";
            }
            else if (dt1.Rows.Count == 5)
            {
                txtReportNo.Text = ddlSubReport.SelectedValue + "/F";
            }
            else if (dt1.Rows.Count == 6)
            {
                txtReportNo.Text = ddlSubReport.SelectedValue + "/G";
            }
            else if (dt1.Rows.Count == 7)
            {
                txtReportNo.Text = ddlSubReport.SelectedValue + "/H";
            }
            else
            {
            }
        }
        else
        {
            txtReportNo.Text = ddlSubReport.SelectedValue + "/A";
        }
    }
    protected void ddlSelectAccountYear_SelectedIndexChanged(object sender, EventArgs e)
    {
        if (!string.IsNullOrEmpty(txtDateOfReceived.Text))
        {
            string DateOfReceived = txtDateOfReceived.Text;
            string[] ValidationCurrentYear = DateOfReceived.Split('-');
            string Month = ValidationCurrentYear[0];
            string Date = ValidationCurrentYear[1];
            string year = ValidationCurrentYear[2];
            int monthI = Convert.ToInt32(Month);
            int YearI = Convert.ToInt32(year);
            int Year1 = YearI + 1;
            int Year0 = YearI - 1;
            
            if (monthI > 3)
            {
                ddlSelectAccountYear.Items.Insert(0, new ListItem(year + "-" + Year1, "0"));
                //if (!IsPostBack)
                //{
                //    ddlSelectAccountYear.SelectedIndex = -1;
                   
                   
                //}
                ddlSelectAccountYear.SelectedIndex = -1;
                ddlSelectAccountYear.DataBind();
            }
            else
            {
                ddlSelectAccountYear.Items.Insert(0, new ListItem(Year0 + "-" + year, "0"));
                //if (!IsPostBack)
                //{
                //    ddlSelectAccountYear.SelectedIndex = -1;
                    
                  
                //}
                ddlSelectAccountYear.SelectedIndex = -1;
                ddlSelectAccountYear.DataBind();
            }

        }
        else
        {
        }
    }  
    protected void btnReport_Click(object sender, EventArgs e)
    {
    }
    protected void btnSellersBuyersname_Click(object sender, EventArgs e)
    {
        Response.Redirect("/ShallerByersname.aspx");

    }
    protected void btnSampleReceivedFrom_Click(object sender, EventArgs e)
    {
        Response.Redirect("/SampleReceivedFrom.aspx");
    }
    protected void btnNameOfSample_Click(object sender, EventArgs e)
    {
        Response.Redirect("/NameOfSample.aspx");
    }
    protected void btnDateOfreceived_Click(object sender, EventArgs e)
    {
        Response.Redirect("/DateOfreceived.aspx");
    }
    protected void txtSealImpression_TextChanged(object sender, EventArgs e)
    {

    }
    protected void gvReportDisplay_RowEditing(object sender, GridViewEditEventArgs e)
    {
        gvReportDisplay.EditIndex = e.NewEditIndex;
        gvReportDisplay.DataBind();
    }
    protected void gvReportDisplay_RowCancelingEdit(object sender, GridViewCancelEditEventArgs e)
    {
        gvReportDisplay.EditIndex = -1;
        gvReportDisplay.DataBind();
    }
    protected void gvReportDisplay_RowUpdating(object sender, GridViewUpdateEventArgs e)
    {
      
        gvReportDisplay.DataBind();
    }
    protected void btnSubreport_Click(object sender, EventArgs e)
    {
        Response.Redirect("/SubReport.aspx");
    }
}
