#实验五：综合性实验

###一、实验目的
1、分析学生选课系统
2、使用GUI窗体及其组件设计窗体界面
3、完成学生选课过程业务逻辑编程
4、基于文件保存并读取数据
5、处理异常

###二、实验要求
1、系统角色分析及类设计
学校有“人员”，分为“教师”和“学生”，教师教授“课程”，学生选择课程。
定义每种角色人员的属性，及其操作方法。
属性示例：
>教师（编号、姓名、性别、所授课程）
学生（编号、姓名、性别、所选课程）
课程（编号、课程名称、上课地点、时间、授课教师）

2、要求:
>（1）设计GUI窗体，支持学生注册、课程新加、学生选课、学生退课、打印学生选课列表等操作。
（2）基于事件模型对业务逻辑编程，实现在界面上支持上述操作。
（3）针对操作过程中可能会出现的各种异常，做异常处理
（4）基于输入/输出编程，支持学生、课程、教师等数据的读写操作。
（5）基于Github.com提交实验，包括实验SRC源文件夹程序、README.MD实验报告文档。

###三、流程图
见图片

###四、实验代码
选课主要代码

		setTitle("选择课程");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);	//X关闭窗口
		setBounds(100, 100, 800, 400);	//将组件大小
		contentPane = new JPanel();	//设置一个与容器相关联的内容面板
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));	//设置组件的边框
		setContentPane(contentPane);	//设置ContentPane
		GridBagLayout gbl_contentPane = new GridBagLayout();	//设置布局
		gbl_contentPane.columnWidths = new int[]{185, 136, 0};
		gbl_contentPane.rowHeights = new int[]{51, 86, 0};
		gbl_contentPane.columnWeights = new double[]{1.0, 0.0, Double.MIN_VALUE};
		gbl_contentPane.rowWeights = new double[]{0.0, 1.0, Double.MIN_VALUE};
		contentPane.setLayout(gbl_contentPane);		
		Label label = new Label("选择课程");
		GridBagConstraints gbc_label = new GridBagConstraints();	//布局
		gbc_label.insets = new Insets(0, 0, 5, 5);
		gbc_label.gridx = 0;
		gbc_label.gridy = 0;
		contentPane.add(label, gbc_label);		
		DefaultListModel listModel=new DefaultListModel();	//创建设置列表数据 
		JList list = new JList(listModel); 
		GridBagConstraints gbc_list = new GridBagConstraints();
		gbc_list.insets = new Insets(0, 0, 0, 5);	//组件间距
		gbc_list.fill = GridBagConstraints.BOTH;	//填充空余
		gbc_list.gridx = 2;	//X2 
		gbc_list.gridy = 0;	//Y0
		contentPane.add(list, gbc_list);
            BufferedReader br = new BufferedReader(new FileReader("D:\\JAVA实验\\classes_teachers.txt"));	//读取文件
            String demo = br.readLine();
            br.close();
            String [] array = demo.split(";"); 
            for (int i=0; i<array.length ;i++) {
        		listModel.addElement(array[i]); 
            }
		JButton btnNewButton = new JButton("选择");	//按钮事件
		GridBagConstraints gbc_btnNewButton = new GridBagConstraints();	//设置布局
		gbc_btnNewButton.gridwidth = 2;
		gbc_btnNewButton.gridx = 1;
		gbc_btnNewButton.gridy = 1;
		contentPane.add(btnNewButton, gbc_btnNewButton);	//面板新加按钮
		btnNewButton.addActionListener(new ActionListener(){
			public void actionPerformed(ActionEvent e) {
				String chosen = (String)list.getSelectedValue()+";";	//只读取string
				 FileWriter writer;
			        	BufferedReader br = new BufferedReader(new FileReader("D:\\JAVA实验\\numbers.txt"));
			            String Student_num = br.readLine();
			            br.close();
			            writer = new FileWriter("D:\\JAVA实验\\" + Student_num +".txt",true);	//利用write方法将字符串写入	            
			            writer.append(chosen); 
			            writer.close();
			        } }
			        
					JOptionPane.showMessageDialog(null, "成功选课！");	//弹个对话框 
				    System.exit(0);

在选课的过程当中主要就是通过将学生选课信息显示出并使用FileWriter的方法使其写到txt文件中去

创建课程主要代码

		setTitle("创建课程");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 450, 300);
		contentPane = new JPanel();
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		GridBagLayout gbl_contentPane = new GridBagLayout();
		gbl_contentPane.columnWidths = new int[]{93, 142, 164, 0};
		gbl_contentPane.rowHeights = new int[]{0, 0, 0, 0, 0, 0, 0, 0, 0};
		gbl_contentPane.columnWeights = new double[]{1.0, 0.0, 0.0, Double.MIN_VALUE};
		gbl_contentPane.rowWeights = new double[]{1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1.0, Double.MIN_VALUE};
		contentPane.setLayout(gbl_contentPane);		
		Label label = new Label("课程编号: ");
		//label.setFont(new Font("Calibri", Font.BOLD | Font.ITALIC, 12));
		GridBagConstraints gbc_label = new GridBagConstraints();
		gbc_label.insets = new Insets(0, 0, 5, 5);
		gbc_label.gridx = 0;
		gbc_label.gridy = 1;
		contentPane.add(label, gbc_label);
		TextField textField = new TextField();
		GridBagConstraints gbc_textField = new GridBagConstraints();
		gbc_textField.fill = GridBagConstraints.BOTH;
		gbc_textField.insets = new Insets(0, 0, 5, 5);
		gbc_textField.gridx = 1;
		gbc_textField.gridy = 1;
		contentPane.add(textField, gbc_textField);
		Label label_1 = new Label("课程名称: ");
		。。。。。。。
		        try {
		            writer = new FileWriter("D:\\JAVA实验\\classes_teachers.txt",true);
		            writer.append(s6); 
		            writer.flush();
		            writer.close();
		        } catch (IOException e1) {
		           //ignore
		        }
				JOptionPane.showMessageDialog(null, "成功创建");
			    System.exit(0);

以上课程的创建和之前学生设立相类似，编号、时间、地点、名称都需要设置其label，最后同样通过FileWriter方法。

系统登陆界面

		setTitle("进入系统");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(200, 200, 550, 350);
		contentPane = new JPanel();
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		GridBagLayout gbl_contentPane = new GridBagLayout();
		gbl_contentPane.columnWidths = new int[]{0, 0, 0, 0};
		gbl_contentPane.rowHeights = new int[]{0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
		gbl_contentPane.columnWeights = new double[]{0.0, 0.0, 1.0, Double.MIN_VALUE};
		gbl_contentPane.rowWeights = new double[]{0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, Double.MIN_VALUE};
		contentPane.setLayout(gbl_contentPane);	
		JRadioButton rdbtnNewRadioButton_1 = new JRadioButton("学生");
		GridBagConstraints gbc_rdbtnNewRadioButton_1 = new GridBagConstraints();
		gbc_rdbtnNewRadioButton_1.insets = new Insets(0, 0, 5, 5);
		gbc_rdbtnNewRadioButton_1.gridx = 1;
		gbc_rdbtnNewRadioButton_1.gridy = 0;
		contentPane.add(rdbtnNewRadioButton_1, gbc_rdbtnNewRadioButton_1);			  
		JLabel lblNewLabel = new JLabel("号码");
此处要有老师的登陆和学生的登陆

###五、实验体会
本次实验又回归到了之前实验的后续，需要根据之前GUI进行修改并引入异常处理，以及基于事件模型对业务逻辑的一个编程。在实验中利用文件的读取利用很好的使学生选课系统更为完善。但是在实验过程中，因为版本问题总是会报很多错出来，需要把自己的版本降低，这块也训练了我分析问题的能力，库的引入本来就不应该报错的地方如果出现了问题就应该去好好查看一下。总之是最后一个实验了，收获颇丰，希望可以得到一个较高的分数并在之后的语言学习中应用到java学习的逻辑。
