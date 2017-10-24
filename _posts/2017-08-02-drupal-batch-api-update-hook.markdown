---
layout: post
title:  "Welcome to Jekyll!"
date:   2017-03-18 08:08:26 +0100
categories: jekyll update
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
+/**
+ * Fix undefined language in body after upgrade.
+ */
+function myproject_core_update_7203(&$sandbox) {
+  if (empty($sandbox)) {
+    $sandbox['progress'] = 0;
+
+    // How many entities will need processing?
+    // Select all nodes that don't have en content but und.
+    $subquery = db_select('field_data_body', 'b')
+      ->fields('b', array('entity_id'))
+      ->condition('b.language', 'en', '=');
+    $res = db_select('field_data_body', 'b')
+      ->fields('b', array('entity_id'))
+      ->condition('b.language', 'und', '=')
+      ->condition('b.entity_id', $subquery, 'NOT IN')
+      ->execute();
+    $count = $res->rowCount();
+
+    if (intval($count) === 0) {
+      // Nothing to do.
+      $sandbox['#finished'] = 1;
+      return;
+    }
+    // Batch 100 items in one go.
+    $sandbox['max'] = ceil($count / 100);
+    $sandbox['chunks'] = array_chunk($res->fetchCol(), 100);
+  }
+
+  $offset = $sandbox['progress'];
+  $batch = $sandbox['chunks'][$offset];
+
+  foreach ($batch as $nid) {
+    $node = node_load($nid);
+
+    if (!empty($node) && isset($node->body[LANGUAGE_NONE]) && !empty($node->body[LANGUAGE_NONE])) {
+      // Do the old switcheroo!
+      $body = $node->body[LANGUAGE_NONE];
+      unset($node->body[LANGUAGE_NONE]);
+      $node->body['en'] = $body;
+      $node->language = 'en';
+      $node->revision = 1;
+      $node->workbench_modetation_state_new = workbench_moderation_state_published();
+      node_save($node);
+    }
+  }
+
+  // Are we done ?
+  $sandbox['progress']++;
+  $sandbox['#finished'] = $sandbox['progress'] / $sandbox['max'];
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
