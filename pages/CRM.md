- #+BEGIN_QUERY
  {:title [:h2 "Last contact"]
    :query [:find ?name ?interval (max ?day)
                 :keys name interval day
                 :where
                   [?jp :block/journal-day ?day]
                   [?mention :block/page ?jp]
                   [?mention :block/refs ?person]
                   [?person :block/original-name ?name] ; gets the name of the page as displayed in Logseq.
                   [?person :block/properties ?prop] ; I'm assuming the use of a page-property here. (i.e. first block on the page)
                   [(get ?prop :contact) ?interval]
    ]
    :result-transform (fn [result] 
      (sort-by 
        (juxt 
          (fn [i] (get i :interval)) 
          (fn [d] (get d :day)) 
        ) result)
    )
    :view (fn [rows]
      [:table 
        [:thead [:tr
          [:th "Name"]
          [:th "Interval"]
          [:th "Date"]
        ] ]
        [:tbody (for [r rows] [:tr
          [:td [:a {:href (str "#/page/" (get r :name))} (get r :name)]]
          [:td (get r :interval)]
          [:td (get r :day)]
        ] ) ]
      ]
    )
  }
  #+END_QUERY
- #+BEGIN_QUERY
  {:title [:h2 "Longer than 7 days"]
    :query [:find (pull ?person [*])
                 :in $ ?dl
                 :where
                   ; all people with a weekly contact interval
                   [?person :block/original-name ?name]
                   [?person :block/properties ?prop]
                   [(get ?prop :contact) ?interval]
                   [(= ?interval "weekly")]
                   ; who are not mentioned on journal pages of the last 7 days
                   (not [?mention :block/refs ?person]
                   [?mention :block/page ?jp]
                   [?jp :block/journal-day ?day]
                   [(>= ?day ?dl)])
    ]
    :inputs [:7d] ; only accepts dynamic days
  }
  #+END_QUERY
- #+BEGIN_QUERY
  {:title [:h2 "Persons list"]
    :query [:find (pull ?p [*])
      :where
        [?p :page/name ?name]
        [(clojure.string/starts-with? ?name "@")]
        ; [?p :block/properties ?prop]
        ; [(get ?prop :contact)] ; optional, only needed if you have @ pages without property contact that you want to exclude.
    ]
  }
  #+END_QUERY