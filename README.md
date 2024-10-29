### 拉霸機
### **說明**
1. 設計一張背景圖當作表單的背景
2. 建立
    * 三個圖片方塊(picturebox)
    * 一個未按和已按拉稈圖示(picturebox)
    * 一個標籤顯示目前可投注總數量(Label)
    * 一個數字按鈕用來設定每次投注量(numericUpDown)
3. 拉霸機上三個圖示
    * 建立pictureBox陣列，儲存三種元素
    * p[1] = pic1
    * p[2] = pic2
    * p[3] = pic3
4. 計時器(timer)控制亂數取圖
    * 每隔0.1秒重新亂數取圖一次
    * 連續20次停止計時
5. 判斷中獎
    * 荔枝代碼 0
    * 星星代碼 1
    * 西瓜代碼 2
    * BAR代碼 3
6. 按下拉稈判斷
    1. 投注量是否大於0 或 投注量是否小於總數量？
    1. 啟動timer計時器，減掉本次投注量，使rndQty無法使用、BtnPic圖示紐失效、BtnPic以圖示(down.jpg)顯示
    1. 出現對話方塊並顯示 "投注有誤"

![image](https://hackmd.io/_uploads/H1qZNz0lye.png)

```chsarp=
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        PictureBox[] p = new PictureBox[4];
        int[] nums = new int[4];
        private void Form1_Load(object sender, EventArgs e)
        {
            pictureBox4.Image = new Bitmap("1315.jpg");
            p[1] = pictureBox1;
            p[2] = pictureBox2;
            p[3] = pictureBox3;
            for (int i = 1; i <= p.GetUpperBound(0); i++)
            {
                p[i].Image = new Bitmap("3.jpg");
                p[i].SizeMode = PictureBoxSizeMode.StretchImage;

            }
            label2.Text = "50";
            timer1.Interval = 100;
        }

        private void pictureBox4_Click(object sender, EventArgs e)
        {
            if (numericUpDown1.Value > 0 && numericUpDown1.Value <= Convert.ToInt32(label2.Text))
            {
                pictureBox4.Image = new Bitmap("1316.jpg");
                timer1.Enabled = true;
                cheat = cheat + 1;
                label2.Text = Convert.ToString(Convert.ToInt32(label2.Text) - numericUpDown1.Value);


            }
            else
            {
                MessageBox.Show("投注有誤");
            }
        }
        int count=0;
        int cheat=0;
        private void timer1_Tick(object sender, EventArgs e)
        {
            Random r = new Random();
            for (int i = 1; i <= p.GetUpperBound(0); i++)
            {
                nums[i] = r.Next(0, 4);
                p[i].Image = new Bitmap(Convert.ToString(nums[i]) + ".jpg");

            }
            label1.Text = count.ToString();
            count += 1;
            if (count == 20)
            {
                timer1.Enabled = false;
                if (cheat % 3==0)
                {
                    nums[1] = nums[2] = nums[3];
                    p[1].Image = p[2].Image = p[3].Image;
                }
                
                if (nums[1] == 0 && nums[2] == 0 && nums[3] == 0)
                {
                    label2.Text = Convert.ToString(Convert.ToInt32(label2.Text) + numericUpDown1.Value * 5);
                    MessageBox.Show("恭喜中獎，投注量×5");
                }
                else if (nums[1] == 1 && nums[2] == 1 && nums[3] == 1)
                {
                    label2.Text = Convert.ToString(Convert.ToInt32(label2.Text) + numericUpDown1.Value * 10);
                    MessageBox.Show("恭喜中獎，投注量×10");
                }
                else if (nums[1] == 2 && nums[2] == 2 && nums[3] == 2)
                {
                    label2.Text = Convert.ToString(Convert.ToInt32(label2.Text) + numericUpDown1.Value * 15);
                    MessageBox.Show("恭喜中獎，投注量×15");
                }
                else if (nums[1] == 3 && nums[2] == 3 && nums[3] == 3)
                {
                    label2.Text = Convert.ToString(Convert.ToInt32(label2.Text) + numericUpDown1.Value * 20);
                    MessageBox.Show("恭喜中獎，投注量×20");
                }
                count = 0;
            }
        }
    }
}

```# slot_machine
