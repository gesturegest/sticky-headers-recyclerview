sticky-headers-recyclerview
===========================

This decorator allows you to easily create section headers for RecyclerViews using a
LinearLayoutManager in either vertical or horizontal orientation.

Download
--------

    compile 'com.timehop.stickyheadersrecyclerview:library:0.4.2@aar'

Usage
-----

In order to implement sticky headers for an adapter, make your `RecyclerView.Adapter` implement `StickyRecyclerHeadersAdapter` and implement the following methods:
```java
public long getHeaderId(int position);
public VH onCreateHeaderViewHolder(ViewGroup parent);
public void onBindHeaderViewHolder(VH holder, int position);
public int getItemCount();
```
Then, decorate the recycler with `StickyRecyclerHeadersDecoration`:
```java
mRecyclerView = (RecyclerView) findViewById(R.id.recyclerview);
mAdapter = new MyStickyRecyclerHeadersAdapter();
mRecyclerView.setAdapter(mAdapter);
mRecyclerView.setLayoutManager(new LinearLayoutManager(context));
mRecyclerView.addItemDecoration(new StickyRecyclerHeadersDecoration(mAdapter));
```

`StickyRecyclerHeadersTouchListener` allows you to listen for clicks on header views.
Simply create an instance of `StickyRecyclerHeadersTouchListener`, set the `OnHeaderClickListener`,
and add the `StickyRecyclerHeadersTouchListener` as a touch listener to your `RecyclerView`.

```java
StickyRecyclerHeadersTouchListener touchListener =
    new StickyRecyclerHeadersTouchListener(recyclerView, headersDecor);
touchListener.setOnHeaderClickListener(
    new StickyRecyclerHeadersTouchListener.OnHeaderClickListener() {
      @Override
      public void onHeaderClick(View header, int position, long headerId) {
        Toast.makeText(MainActivity.this, "Header position: " + position + ", id: " + headerId,
            Toast.LENGTH_SHORT).show();
      }
    });
mRecyclerView.addOnItemTouchListener(touchListener);
```

=======
The StickyHeaders aren't aware of your adapter so if you must notify them when your data set changes.

```java
    mAdapter.registerAdapterDataObserver(new RecyclerView.AdapterDataObserver() {
      @Override public void onChanged() {
        headersDecor.invalidateHeaders();
      }
    });
```

Item animators don't play nicely with RecyclerView decorations, so your mileage with that may vary.

Compatibility
-------------

This should work in API 14+.

>>>>>>> 8da3abdd108130930c31537d9537cf503fc022aa
Known Issues
------------

* Header views aren't recycled at this time
* ItemAnimators issues

* The header views are drawn to a canvas, and are not actually a part of the view hierarchy. As such, they can't have touch states, and you may run into issues if you try to load images into them asynchronously.

Version History
---------------
0.4.2 (8/21/2015) - Add support for reverse `ReverseLayout` in `LinearLayoutManager` by [AntonPukhonin](https://github.com/AntonPukhonin)

0.4.1 (6/24/2015) - Fix "dancing headers" by DarkJaguar91

0.4.0 (4/16/2015) - Code reorganization by danoz73, fixes for different sized headers, performance improvements

0.3.6 (1/30/2015) - Prevent header clicks from passing on the touch event
<<<<<<< HEAD
=======

0.3.5 (12/12/2014) - Add StickyRecyclerHeadersDecoration.invalidateHeaders() method

0.3.4 (12/3/2014) - Fix issues with rendering of header views with header ID = 0

0.3.3 (11/13/2014) - Fixes for padding, support views without headers

0.3.2 (11/1/2014) - Bug fixes for list items with margins and deleting items

0.2 (10/3/2014) - Add StickyRecyclerHeadersTouchListener

0.1 (10/2/2014) - Initial Release
>>>>>>> 8da3abdd108130930c31537d9537cf503fc022aa
