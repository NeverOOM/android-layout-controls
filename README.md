#ViewPagerIndicator+viewpager的简单使用，不需要导入Library包
    <div class="blog-body" id="blogBody">
                                    <val data-name="blog_content_type" data-value="richtext"></val>
                    <div class='BlogContent'>
                        <p>ViewPagerIndicator作为一款分页指标小部件兼容ViewPager，封装上做得非常不错，目前已为众多知名应用所使用。</p> 
<p>ViewPagerIndicator+viewpager实现如下效果：（注：不需要导入或引入啥包就可实现）</p> 
<p>&nbsp; &nbsp; &nbsp;&nbsp;<img alt="" height="233" src="https://static.oschina.net/uploads/space/2016/1207/160527_AcpJ_2945455.gif" width="317"></p> 
<p>六个类就可实现上图效果</p> 
<p><img alt="" height="143" src="https://static.oschina.net/uploads/space/2016/1207/162238_9zv7_2945455.png" width="218"></p> 
<p>activity_main.xml</p> 
<pre><code class="language-html">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="fill_parent"&gt;

    &lt;com.viewpagerindicator.TabPageIndicator
        android:id="@+id/indicator"
        android:layout_height="wrap_content"
        android:layout_width="match_parent"
        /&gt;
    &lt;android.support.v4.view.ViewPager
        android:id="@+id/pager"
        android:layout_width="fill_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        /&gt;
&lt;/LinearLayout&gt;</code></pre> 
<p>MainActivity.java</p> 
<pre><code class="language-java">public class MainActivity extends FragmentActivity {
    private static final String[] CONTENT = new String[] { "推荐", "热点", "视频", "本地", "科技", "健康" };

    private List&lt;Fragment&gt; list=new ArrayList&lt;Fragment&gt;();
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        FragmentPagerAdapter adapter = new GoogleMusicAdapter(getSupportFragmentManager());

        ViewPager pager = (ViewPager)findViewById(R.id.pager);
        pager.setAdapter(adapter);

        TabPageIndicator indicator = (TabPageIndicator)findViewById(R.id.indicator);
        indicator.setViewPager(pager);
    }

    class GoogleMusicAdapter extends FragmentPagerAdapter {
        public GoogleMusicAdapter(FragmentManager fm) {
            super(fm);
            list.add(new TestFragment(CONTENT[0]));
            list.add(new TestFragment(CONTENT[1]));
            list.add(new TestFragment(CONTENT[2]));
            list.add(new TestFragment(CONTENT[3]));
            list.add(new TestFragment(CONTENT[4]));
            list.add(new TestFragment(CONTENT[5]));
        }

        @Override
        public Fragment getItem(int position) {
            return list.get(position);
        }

        @Override
        public CharSequence getPageTitle(int position) {
            return CONTENT[position % CONTENT.length].toUpperCase();
        }

        @Override
        public int getCount() {
            return CONTENT.length;
        }
    }
}</code></pre> 
<p>Fragment.Java</p> 
<pre><code class="language-java">public final class TestFragment extends Fragment {
  
	private String s;

	public TestFragment(String s)
	{
		this.s=s;
	}
	
    @Override
    public View onCreateView(LayoutInflater inflater,  ViewGroup container,  Bundle savedInstanceState) {

        return inflater.inflate(R.layout.fragment_news, container, false);
    }

    @Override
    public void onActivityCreated( Bundle savedInstanceState) {
        // TODO Auto-generated method stub
        super.onActivityCreated(savedInstanceState);
        View view=getView();
        TextView te=(TextView)view.findViewById(R.id.textView1);
        te.setText(s);
    }

    public void initView() {
    }
}</code></pre> 
<p>工具类代码代码太多未给出，直接下载即可。</p> 
