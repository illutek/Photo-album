# Photo albums
## Drupal8
Dit alles zonder extra modules afgezien van de colorbox.

### Werkwijze
1. Inhoudstype photo_album met 2 velden (intro text-field en afbeeldings-veld)
2. view photo_album, inhoud - teaser een menu-link en de gebruikelijke filters
3. Vijftal twig files alle gegroepeerd in templates/photo  

   node--photo-album--teaser.html.twig   
   hier wat code toegevoegd om de titel van het album in te korten 
   tot 20 karakters en enkel te tonen van de eerste foto van elk album
   ```twig
   {{ content.field_album_pics[0] }}
   ```
   
   node--photo-album--full.html.twig  
   Om alle foto's te printen als ook de intro tekst  
   ```twig
   <div class="photos__content--intro">
     {{ content.field_album_info }}
   </div>   
   <div{{ content_attributes.addClass('photos__content--img') }}>
     {{ content.field_album_pics }}
   </div>
   ```
   views-view--photo-albums.html.twig  
   Dit om een eigen class toe te voegen aan de parent container van de in stap 2 gemaakte view  
   Doe dit liever op dit niveau zou dit ook kunnen in de view zelf veronder stel ik.  
   Op deze container met flex alle album covers langs elkaar.
   
   views-view-unformatted--photo-albums.html.twig  
   Hier een class om de flex-items een width en wat extra opmaak mee te geven.  
   
   field--field-album-pics.html.twig  
   De parent container van alle afbeeldingen op de volledige node met css-grid  
   ```css
   .photo__field--items {
       display: grid;
       grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
       grid-gap: 10px;
       align-items: stretch;
   }
   ```
   Het is op deze file dat de title-tag onder elke afbeelding wordt geprint.
   ```twig
   <div class="photo__field--items-container">
     <div{{ item.attributes.addClass('field__item photo__field--item') }}>
       {{ item.content }}
     </div>
   
     <div class="photo__title">
       {{ item.content['#item'].title }}
     </div>
   </div>
   ```
   
   Elk afbeelding met zijn title-tag zijn ook weer flex-items, dit om de tekst steeds onderaan het panel te tonen.
   
   
   
   
   