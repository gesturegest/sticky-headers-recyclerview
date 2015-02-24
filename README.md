sticky-headers-recyclerview
===========================

This decorator allows you to easily create section headers for RecyclerViews using a
LinearLayoutManager in either vertical or horizontal orientation.

Download
--------

    compile 'com.timehop.stickyheadersrecyclerview:library:0.3.6@aar'

Usage
-----

In order to implement sticky headers for an adapter, make your `RecyclerView.Adapter` implement `StickyRecyclerHeadersAdapter` and implement the necessary methods:

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

If you are interested in listening for clicks, `StickyRecyclerHeadersTouchListener` allows you to listen for clicks on header views: create an instance of `StickyRecyclerHeadersTouchListener`, set the `OnHeaderClickListener`,
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

Known Issues
------------

* The header views aren't recycled at this time.  Contributions are most welcome.

* I haven't tested this with ItemAnimators yet.

Version History
---------------
0.3.6 (1/30/2015) - Prevent header clicks from passing on the touch event

0.3.5 (12/12/2014) - Add StickyRecyclerHeadersDecoration.invalidateHeaders() method

0.3.4 (12/3/2014) - Fix issues with rendering of header views with header ID = 0

0.3.3 (11/13/2014) - Fixes for padding, support views without headers

0.3.2 (11/1/2014) - Bug fixes for list items with margins and deleting items

0.2 (10/3/2014) - Add StickyRecyclerHeadersTouchListener

0.1 (10/2/2014) - Initial Release
