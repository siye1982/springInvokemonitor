ʹ��telnet���ӵ�����spring��Ӧ����ִ�������е�bean�����ⷽ��

ʹ��telnet���ӵ�����spring��Ӧ����ִ�����������õ��κ�bean�����ⷽ���������������ĳ�������Ƿ�ִ�������⣬��Ӧʱ����٣������������п��ԺܺõĶ�λ����ط����Ƿ�������⡣

�����ڣ�https://github.com/zhwj184/springInvokemonitor

	git clone git@github.com:zhwj184/springInvokemonitor.git 

	maven clean install

pom������

	<dependency>
		<groupId>org.zhwj184</groupId>
		<artifactId>springinvokemonitor</artifactId>
		<version>1.0-SNAPSHOT</version>
	</dependency>
	
ʹ�÷�ʽ����spring�������ļ�������������bean���ɡ�

	<bean id="ServiceInvokeClient" class="org.zhwj184.ServiceInvokeClient" />
	
ʹ��ʾ������дһ��service TestBean������������������add��addBean

	import com.alibaba.fastjson.JSON;

	public class TestBean {

		public float add(int a, float b){
			return a + b;
		}
		
		public A addBean(A a, A b){
			A c = new A();
			c.setC(a.getC() + b.getC());
			c.setD(a.getD() + b.getD());
			return c;
		}
		public static void main(String[] args) {
			A c = new A();
			c.setC(23);
			c.setD(323.34);
			System.out.println(JSON.toJSON(c));
		}
		
	}

	class A{
		int c ;
		double d;
		public int getC() {
			return c;
		}
		public void setC(int c) {
			this.c = c;
		}
		public double getD() {
			return d;
		}
		public void setD(double d) {
			this.d = d;
		}
		
	}
	
Ȼ����spring�����ļ� service.xml���

	<bean id="testBean" class="org.zhwj184.TestBean" />
	<bean id="ServiceInvokeClient" class="org.zhwj184.ServiceInvokeClient" />
	
дһ�������ִ࣬�����main������

	import org.springframework.context.support.ClassPathXmlApplicationContext;

	public class MainTest {

		/**
		 * @param args
		 * @throws InterruptedException 
		 */
		public static void main(String[] args) throws InterruptedException {
			ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("classpath:service.xml");
			Thread.sleep(100000000);
		}

	}

Ȼ��ͨ��telnet������������ϣ��������д��ڣ�����telnet localhost 12667������֮������ls bean���ƣ����ɲ�ѯ���bean�����з�����ʹ��invoke beanname.method(param1,param2) ִ��ĳ���������������Ϊbean�����ʹ��json��ʽ���룬����֮����;�ָ�


	======================================================

	   Welcome to Telnet Server: Version 1.0

	======================================================

	List of possible commands:

	Status: displays the status of the server
	cd : [ cd /usr/local]
	pwd: displays the working directory
	ls: displays list of files in the working directory
	mkdir : [ mkdir /usr/local/tmp]
	exit : quit this programme

	ls testBean
	org.zhwj184.A org.zhwj184.TestBean.addBean(org.zhwj184.A,org.zhwj184.A)
	void org.zhwj184.TestBean.main([Ljava.lang.String;)
	float org.zhwj184.TestBean.add(int,float)
	int org.zhwj184.TestBean.hashCode()
	java.lang.Class org.zhwj184.TestBean.getClass()
	void org.zhwj184.TestBean.wait(long,int)
	void org.zhwj184.TestBean.wait()
	void org.zhwj184.TestBean.wait(long)
	boolean org.zhwj184.TestBean.equals(java.lang.Object)
	java.lang.String org.zhwj184.TestBean.toString()
	void org.zhwj184.TestBean.notify()
	void org.zhwj184.TestBean.notifyAll()

	invoke testBean.add(1;2.4)
	result:java.lang.Float 3.4
	run time: 0ms

	invoke testBean.addBean({"c":23,"d":323.34};{"c":3433,"d":3232433.34})
	result:org.zhwj184.A {"c":3456,"d":3232756.6799999997}
	run time: 0ms

�����������spring�������κ�bean�����ⷽ����ִ�з������������ؽ���Ƿ��Ԥ�ڵ�һ�¡�һ���������������Ի����ܶ��������������ݿ⣬����ȣ�����һ�����������ϳ�������һ�㶼����֪��������ͨ��ִ�з����Ϳ��Կ�������Ƿ���ȷ�����Ҳ鿴ĳ��������ִ��ʱ�����������Ƿ����������⡣

��������Ĵ���ֻ�Ǽ�����ʾ���������й��ڲ��������ͣ����ƥ�䷴��ȿ��ܲ�������Ҳû�в��Եúܳ�֣�����������Ȥ�Ļ����������ҡ�