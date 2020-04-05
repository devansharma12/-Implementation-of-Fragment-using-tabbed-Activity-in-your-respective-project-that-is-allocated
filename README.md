# -Implementation-of-Fragment-using-tabbed-Activity-in-your-respective-project-that-is-allocated
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android "
xmlns:app="http://schemas.android.com/apk/res-auto" android:layout_width="match_parent" android:layout_height="match_parent" android:orientation="vertical"><include layout="@layout/app_bar"
/><android.support.design.widget.TabLayout android:id="@+id/tabLayout" android:layout_width="match_parent" android:layout_height="wrap_content" android:minHeight="?actionBarSize" app:tabGravity="fill" app:tabIndicatorColor="@color/white" app:tabIndicatorHeight="4dp" app:tabBackground="@color/colorPrimary"
app:tabMode="fixed"></android.support.design.widget.TabLa yout><android.support.v4.view.ViewPager android:id="@+id/viewPager" android:layout_width="match_parent" android:layout_height="match_parent"></android.support.v4. view.ViewPager></LinearLayout>
 
TabAdapter.java
package com.example.demoproject;
import android.support.annotation.Nullable; import android.support.v4.app.Fragment;
import android.support.v4.app.FragmentManager;
import android.support.v4.app.FragmentStatePagerAdapter; import java.util.ArrayList;
import java.util.List;public class TabAdapter extends FragmentStatePagerAdapter {
private final List<Fragment> mFragmentList = new ArrayList<>(); private final List<String> mFragmentTitleList = new ArrayList<>();TabAdapter(FragmentManager fm) {
super(fm);
}@Override
public Fragment getItem(int position) { return mFragmentList.get(position);
}public void addFragment(Fragment fragment, String title) { mFragmentList.add(fragment);
mFragmentTitleList.add(title);
}@Nullable @Override
public CharSequence getPageTitle(int position) { return mFragmentTitleList.get(position);
}@Override
public int getCount() { return mFragmentList.size();
}
}

DemoActivity.java

package com.example.demoproject; import android.os.Bundle;
import android.support.design.widget.TabLayout; import android.support.v4.view.ViewPager;
import android.support.v7.app.AppCompatActivity; import android.view.LayoutInflater;
import android.view.View;
import android.widget.TextView;public class DemoActivity extends AppCompatActivity {private TabAdapter adapter;
 
private TabLayout tabLayout;
private ViewPager viewPager;@Override
protected void onCreate(Bundle savedInstanceState) { super.onCreate(savedInstanceState); setContentView(R.layout.activity_demo);
viewPager = (ViewPager) findViewById(R.id.viewPager); tabLayout = (TabLayout) findViewById(R.id.tabLayout);adapter = new TabAdapter(getSupportFragmentManager(), this); adapter.addFragment(new Tab1Fragment(), "Home"); adapter.addFragment(new Tab2Fragment(), "Medicine"); adapter.addFragment(new Tab3Fragment(), "Time");viewPager.setAdapter(adapter); tabLayout.setupWithViewPager(viewPager);highLightCurrent Tab(0); // for initial selected tab viewviewPager.addOnPageChangeListener(new ViewPager.OnPageChangeListener() {
@Override
public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {
}@Override
public void onPageSelected(int position) { highLightCurrentTab(position); // for tab change
}@Override
public void onPageScrollStateChanged(int state) {
}
});
}private void highLightCurrentTab(int position) { for (int i = 0; i < tabLayout.getTabCount(); i++) { TabLayout.Tab tab = tabLayout.getTabAt(i); assert tab != null;
tab.setCustomView(null); tab.setCustomView(adapter.getTabView(i));
}TabLayout.Tab tab = tabLayout.getTabAt(position); assert tab != null;
 
tab.setCustomView(null); tab.setCustomView(adapter.getSelectedTabView(position));
}
}






Output:


