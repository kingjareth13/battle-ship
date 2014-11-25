
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Linq;
using System.Drawing;
using System.Text;
using System.Windows.Forms;

namespace BattleShip
{
    public partial class frmBattleShip : Form
    {
        bool turn = true;
        int turn_count = 0;
        int[,] Your_Board = new int[10, 10] { { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 }, };
        int i, j;
        System.Windows.Forms.Panel[,] Coords = new System.Windows.Forms.Panel[10, 10] { { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null }, { null, null, null, null, null, null, null, null, null, null } };
        

        public frmBattleShip()
        {
            InitializeComponent();
        }
        Color Water = Color.MidnightBlue;
        Color Hit = Color.Tomato;
        Color Miss = Color.White;
        Color Ship = Color.OldLace;
        Color myEnter = Color.IndianRed;
        int myPanelCount = 0;
        

        private void btnWaterMake_Click(object sender, EventArgs e)
        {
            ClearWater();
            MakeWater();
        }

        private void ClearWater()
        {
            int WaterClear = 0;

            for (int i = 0; i < this.Controls.Count; i++)
            {
                Control control = this.Controls[i];

                if (control is Panel)
                {
                    Panel panel = (Panel)control;

                        i--;
                        WaterClear++;
                        panel.Dispose();
                    
                }
            }
            GC.Collect();
        }

        private void MakeWater()
        {
            const int CGridCount = 10;
            int myPanelSize = (this.rctngleSizing.Width) / CGridCount;
            for (int iCol = 0; iCol < CGridCount; iCol++)
            {
                for (int iRow = 0; iRow < CGridCount; iRow++)
                {
                    Panel panel = new Panel();

                    panel.Height = myPanelSize;
                    panel.Width = myPanelSize;
                    panel.Left = iRow * myPanelSize;
                    panel.Top = iCol * myPanelSize;
                    panel.Tag = Water;
                    panel.BackColor = Water;
                    panel.BorderStyle = BorderStyle.Fixed3D;
                    panel.ForeColor = Color.Thistle;
                    panel.Parent = this.rctngleSizing;

                    panel.MouseEnter += new EventHandler(panel_MouseEnter);
                    panel.MouseLeave += new EventHandler(panel_MouseLeave);
                    panel.MouseClick += new MouseEventHandler(panel_MouseClick);
                }
            }
        }

        private void panel_MouseLeave(object sender, EventArgs e)
        {
            Panel panel = (Panel)sender;
            Color color = (Color)panel.Tag;
            panel.BackColor = color;
        }

        private void panel_MouseClick(object sender, EventArgs e)
        {
            Panel panel = (Panel)sender;

            if ((Color)panel.Tag == Water)
            {
                panel.Tag = Ship;
                ++myPanelCount;

                    if (myPanelCount > 17)
                    {
                        MessageBox.Show("Bruh, too many ships!");
                    }
            }

            else
            {
                panel.Tag = Water;
            }

            panel.BackColor = (Color)panel.Tag;
            
        }

        private void panel_MouseEnter(object sender, EventArgs e)
    {
            Panel panel = (Panel)sender;

            if (panel.BackColor != Ship)
            {
                panel.BackColor = myEnter;
            }
        }


         void newToolStripMenuItem_Click(object sender, EventArgs e)
        {

        }

        private void frmBattleShip_Load(object sender, EventArgs e)
        {

        }

        private void quitToolStripMenuItem_Click(object sender, EventArgs e)
        {
            MessageBox.Show("Thanks for Playing");
            this.Close();
        }

        private void resetToolStripMenuItem_Click(object sender, EventArgs e)
        {
            winCount.Text = ("0");
            loseCount.Text = ("0");
            hitCount.Text = ("0");
            missCount.Text = ("0");
            turnCount.Text = ("0");

        }


        private void turnCount_Click(object sender, EventArgs e)
        {
            if (turnCount.Text == "40")
            {
                MessageBox.Show("You are bad at this game if you have not Won by now!");
            }
        }

        private void btnView_Click(object sender, EventArgs e)
        {

        }

        private void howToPlayToolStripMenuItem_Click(object sender, EventArgs e)
        {

        }

        private void frmBattleShip_Load_1(object sender, EventArgs e)
        {

        }

    }
}
