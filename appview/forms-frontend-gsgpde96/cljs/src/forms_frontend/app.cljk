(ns forms-frontend.app
  "Forms Frontend — reagent + re-frame view built from jp-go-dds hiccup.

  This is a faithful port of the former Svelte scaffold (`App.svelte`): a
  single centered heading + message, no interactivity beyond mount. State
  lives in re-frame (`::initialize` event, `::title`/`::subtitle` subs) so the
  scaffold is honest about the stack it now runs on, not because this screen
  needs mutable state yet — the next real feature (a forms entity view) grows
  this db instead of replacing a no-op one."
  (:require [reagent.dom :as rdom]
            [re-frame.core :as rf]
            [jp-go-dds.core :as dds]))

(def initial-db
  {:title "forms-frontend-gsgpde96"
   :subtitle "ClojureScript entry scaffold (reagent + re-frame + jp-go-dds)."})

(rf/reg-event-db
 ::initialize
 (fn [_ _] initial-db))

(rf/reg-sub ::title (fn [db _] (:title db)))
(rf/reg-sub ::subtitle (fn [db _] (:subtitle db)))

(defn view []
  (let [title @(rf/subscribe [::title])
        subtitle @(rf/subscribe [::subtitle])]
    [:main
     (dds/container
      (dds/section {}
        [:div {:class "dds-ext-hero dds-ext-center"}
         (dds/heading 1 title)
         [:p {:class "dds-ext-lead"} subtitle]]))]))

(defn ^:dev/after-load render! []
  (rdom/render [view] (.getElementById js/document "app")))

(defn ^:export main []
  (rf/dispatch-sync [::initialize])
  (render!))
