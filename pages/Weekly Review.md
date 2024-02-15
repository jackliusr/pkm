query-table:: false
query-sort-by:: block
query-sort-desc:: true
#+BEGIN_QUERY
  {:title "Reflections in the Past 7 days"
   :query [:find (pull ?b [*])
         :in $ ?start ?today ?tag
         :where
         [?b :block/page ?p]
         [?p :page/journal-day ?d]
         [(>= ?d ?start)]
         [(<= ?d ?today)]
         [?b :block/ref-pages ?rp]
         [?rp :block/name ?tag]]
   :inputs [:7d-before :today "reflections"]}
  #+END_QUERY

- #+BEGIN_QUERY
  {
   :title [:b "All page changed in the past 7 days"]
  :query [:find (pull ?p [*])
           :in $ ?start ?today
           :where
           [?p :block/journal-day ?d]
           [(>= ?d ?start)]
           [(<= ?d ?today)]
           [?b :block/page ?p]
           ]
   :inputs [:7d-before :today]
  }
  #+END_QUERY
-