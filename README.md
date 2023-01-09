//delete btn
            var senderGrid = (DataGridView)sender;
            if (senderGrid.Columns[e.ColumnIndex] is DataGridViewButtonColumn && e.RowIndex >= 0)
            {
                ID = Convert.ToInt32(dataGridView1.Rows[e.RowIndex].Cells[2].Value.ToString());
                if (ID == 0)
                {
                    MessageBox.Show("Please select a record to delete");
                    return;
                }
                string query = "DELETE FROM test_table WHERE id = @ids";
                using (SqlCommand cmd = new SqlCommand(query, con))
                {
                    cmd.Parameters.AddWithValue("@ids", ID);
                    con.Open();
                    cmd.ExecuteNonQuery();
                    con.Close();
                }
                MessageBox.Show("Record deleted successfully!");
                DisplayData();
                ClearData();
            }
