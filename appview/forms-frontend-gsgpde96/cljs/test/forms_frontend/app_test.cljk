(ns forms-frontend.app-test
  "Real assertions over the re-frame event/sub logic — not just a placeholder
  `(is true)` (the Svelte-era `test/forms.test.ts` was exactly that)."
  (:require [cljs.test :refer [deftest is testing]]
            [re-frame.core :as rf]
            [re-frame.db :as rf-db]
            [forms-frontend.app :as app]))

(defn- dispatch-sync-fresh!
  "Re-frame keeps a single global app-db; reset it before each test so tests
  don't depend on run order."
  [event]
  (reset! rf-db/app-db {})
  (rf/dispatch-sync event))

(deftest initialize-sets-title-and-subtitle
  (testing "::initialize seeds the db with the ported scaffold copy"
    (dispatch-sync-fresh! [::app/initialize])
    (is (= "forms-frontend-gsgpde96" @(rf/subscribe [::app/title])))
    (is (= "ClojureScript entry scaffold (reagent + re-frame + jp-go-dds)."
           @(rf/subscribe [::app/subtitle])))))

(deftest initial-db-matches-what-initialize-produces
  (testing "the event handler and the constant it returns stay in sync"
    (dispatch-sync-fresh! [::app/initialize])
    (is (= (:title app/initial-db) @(rf/subscribe [::app/title])))
    (is (= (:subtitle app/initial-db) @(rf/subscribe [::app/subtitle])))))
