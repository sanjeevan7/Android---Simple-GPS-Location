Android - Simple Custom List View With Image

In this tutorial we will create a Simple Custom List View With Image using Android. This simple app display a list with image using custom array. Android is basically a piece of software which allows your hardware to function. It used in several gadget like smartphone, tablet, and even television. The android is an open source operating system it's free and user friendly to mobile developers. So let's now do the coding...
Getting Started:
First you will have to download & install the Android Development IDE (Android Studio or Eclipse). Android Studio is an open source development feel free to develop your things.

Layout Design
We will now create the design for the application, first locate the layout file called activity_main.xml, this is the default name when create a new activity. Then write these codes inside your layout file.
1.	<?xml version="1.0" encoding="utf-8"?>
2.	<RelativeLayout xmlns:android="<a href="http://schemas.android.com/apk/res/android"
3.	" rel="nofollow">http://schemas.android.com/apk/res/android"
4.	</a>    xmlns:tools="<a href="http://schemas.android.com/tools"
5.	" rel="nofollow">http://schemas.android.com/tools"
6.	</a>    android:layout_width="match_parent"
7.	    android:layout_height="match_parent"
8.	    tools:context="com.razormist.simplelistviewwithimage.MainActivity">
9.
10.	    <ListView
11.	        android:layout_width="match_parent"
12.	        android:layout_height="match_parent"
13.	        android:id="@+id/lv_content"/>
14.
15.	</RelativeLayout>
Now that we're done with the main layout we will create then a layout that display the value of the list. First right click on resource then create a new layout resource namely laptop_list then write these codes inside your layout file.
1.	<?xml version="1.0" encoding="utf-8"?>
2.	<LinearLayout xmlns:android="<a href="http://schemas.android.com/apk/res/android"
3.	" rel="nofollow">http://schemas.android.com/apk/res/android"
4.	</a>    xmlns:app="<a href="http://schemas.android.com/apk/res-auto"
5.	" rel="nofollow">http://schemas.android.com/apk/res-auto"
6.	</a>    android:orientation="horizontal" android:layout_width="match_parent"
7.	    android:layout_height="match_parent">
8.
9.
10.	    <LinearLayout
11.	        android:orientation="horizontal"
12.	        android:layout_width="match_parent"
13.	        android:layout_height="wrap_content" >
14.
15.	    <TextView
16.	        android:id="@+id/tv_list"
17.	        android:layout_width="wrap_content"
18.	        android:layout_height="wrap_content"
19.	        android:text="TextView"
20.	        android:layout_marginTop="30dp"
21.	        android:fontFamily="monospace" />
22.
23.	        <LinearLayout
24.	            android:orientation="horizontal"
25.	            android:layout_width="match_parent"
26.	            android:layout_height="wrap_content"
27.	            android:gravity="right">
28.
29.	            <ImageView
30.	                android:id="@+id/iv_image"
31.	                android:layout_width="wrap_content"
32.	                android:layout_height="wrap_content"
33.	                 app:srcCompat="@mipmap/ic_launcher"
34.	            android:padding="3dp"/>
35.
36.	        </LinearLayout>
37.	    </LinearLayout>
38.
39.	</LinearLayout>
Android Manifest File
The Android Manifest file provides essential information about your app to the Android system in which the system must required before running the code. It describe the overall information about the application. It contains some libraries that needed to access the several method within the app.
1.	<?xml version="1.0" encoding="utf-8"?>
2.	<manifest xmlns:android="<a href="http://schemas.android.com/apk/res/android"
3.	" rel="nofollow">http://schemas.android.com/apk/res/android"
4.	</a>    package="com.razormist.simplelistviewwithimage">
5.
6.	    <application
7.	        android:allowBackup="true"
8.	        android:icon="@mipmap/ic_launcher"
9.	        android:label="@string/app_name"
10.	        android:roundIcon="@mipmap/ic_launcher_round"
11.	        android:supportsRtl="true"
12.	        android:theme="@style/AppTheme">
13.	        <activity android:name=".MainActivity"
14.	            android:configChanges="orientation"
15.	            android:screenOrientation="portrait">
16.	            <intent-filter>
17.	                <action android:name="android.intent.action.MAIN" />
18.
19.	                <category android:name="android.intent.category.LAUNCHER" />
20.	            </intent-filter>
21.	        </activity>
22.	    </application>
23.	</manifest>
Creating the Custom Adapter
This code handle the list of data that will be needed to display. First create a new java file namely ListHandler, then open the newly create file and extend the class by adding extends ArrayAdapter. Next write these variables inside the ListHandler class
1.	String[] name_list;
2.	int[] laptop;
3.	Context context;
After assigning the variables we will now create a certain methods to handle each data that will be listed. To do that write these methods inside the class.
1.	public ListHandler(Context context, String[] name_list, int[] laptop) {
2.	        super(context, R.layout.laptop_list);
3.	        this.name_list = name_list;
4.	        this.laptop = laptop;
5.	        this.context = context;
6.	    }
7.
8.	    @Override
9.	    public int getCount() {
10.	        return name_list.length;
11.	    }
12.
13.	    @NonNull
14.	    @Override
15.	    public View getView(int position, View convertView, ViewGroup parent) {
16.	        TagHolder tagHolder = new TagHolder();
17.	        if(convertView == null) {
18.	            LayoutInflater inflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
19.	            convertView = inflater.inflate(R.layout.laptop_list, parent, false);
20.	            tagHolder.iv_image = (ImageView) convertView.findViewById(R.id.iv_image);
21.	            tagHolder.tv_list = (TextView) convertView.findViewById(R.id.tv_list);
22.	            convertView.setTag(tagHolder);
23.	        }else{
24.	            tagHolder = (TagHolder)convertView.getTag();
25.	        }
26.
27.	        tagHolder.iv_image.setImageResource(laptop[position]);
28.	        tagHolder.tv_list.setText(name_list[position]);
29.	        return convertView;
30.	    }
31.
32.	    static class TagHolder{
33.	        ImageView iv_image;
34.	        TextView tv_list;
35.
36.	    }
The Main Function
This code contains the main function of the application. This code will automatically call the list method to display it inside the resource layout. To start with first locate your MainActivity java file and open it, then write this variable inside the MainActivity class.
1.	 ListView lv_content;
2.
3.	    String[] name_list = {
4.	            "ASUS VivoBook Max X441UR",
5.	            "Acer Aspire One D270-268",
6.	            "Lenovo Ideapad 100S 11",
7.	            "Dell Inspiron 11-3162",
8.	            "HP 11-D002TU",
9.	            "MSI GV62 7RC",
10.	            "Sony Vaio VPCW126AG"
11.	    };
12.
13.	    int[] laptop = {
14.	            R.drawable.asus_vivobook_max_x441ur_l,
15.	            R.drawable.acer_aspire_one_d270_268_l,
16.	            R.drawable.dell_inspiron_11_3162_l,
17.	            R.drawable.lenovo_ideapad_100s_11_ph_l,
18.	            R.drawable.hp_11_d002tu_l,
19.	            R.drawable.msi_gv62_7rc_l,
20.	            R.drawable.sony_vpcw_126ag_l_5
21.	    };
Finally, initialize the require methods inside the onCreate method to run the application.
1.	lv_content = (ListView)findViewById(R.id.lv_content);
2.	        ListHandler listHandler = new ListHandler(MainActivity.this, name_list, laptop);
3.	        listHandler.sort(new Comparator<String>() {
4.	            @Override
5.	            public int compare(String lhs, String rhs) {
6.	                return lhs.compareTo(rhs);
7.	            }
8.	        });
9.	        lv_content.setAdapter(listHandler);
Try to run the app and see if it worked.
There you have it we have created a Simple Custom List View With Image using Android. I hope that this tutorial help you to what you are looking for. For more updates and tutorials just kindly visit this site. Enjoy Coding

