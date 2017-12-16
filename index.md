    
  {%section 'resources-section'%} 
 
  <div class="row custom-filter"> 
   {%section 'resource-filter'%}
   {%include 'resource-filter'%}
  </div>

 


 <script>
   $(function() { 
    var  activeCategory =  $('.active-filter[data-group="category"]').data('handle');
    var  activeCountry  =  $('.country-list option:selected').data('handle');
   $(document).on('change', '.country-list', function(e){
     e.preventDefault();
     el = $('option:selected');
     activeCountry = el.data('handle');
     filter_data();
   });
     
     $(document).on('click', '.clear-country', function(e){
     e.preventDefault();
     activeCountry = '';
     filter_data();
   });
       
     
   $(document).on('click', '.cat-option', function(e){
     e.preventDefault();
     el = $(this);
     activeCategory = el.data('handle');
     filter_data(); 
   });
     
       $(document).on('click', '.clear-category', function(e){
     e.preventDefault();
     el = $(this);
     activeCategory = '';
     filter_data(); 
   });
   		
   function filter_data(){
    
      var base_url = window.location.origin+'/blogs/resources/';
      var slug = '';
     if(activeCategory || activeCountry){
        slug += 'tagged/';
     }  
     
     if(activeCategory){
       slug += activeCategory;   
     }
     
     if(activeCategory && activeCountry){
        slug += '+';
     } 
     
     if(activeCountry){
       slug += activeCountry;   
     }
     var get_url = base_url+slug;
      $('.resource-right').html('<div class="_jsLoaderDiv"><img class="_jsLoader" src="https://cdn.shopify.com/s/files/1/2358/5863/t/5/assets/loading.gif" ></div>');
      $.get(get_url, function(data){
	    $content =  $(data).find('.custom-filter').html();
        $('.custom-filter').html($content);
        history.pushState('', '', get_url);
        
      });
   }  
   });
   </script>


<script>

window.onscroll = function (e) {  
 var h1 = $(window).scrollTop() + $(window).height() +300 ;
  var h2 = $(document).height();
//   console.log(h1);
//   console.log(h2);
  
  if(h1 >= h2) {
//       $(".custom-sidebar").addClass("sticky-fix-bottom");
  }else{
//     $(".custom-sidebar").removeClass("sticky-fix-bottom");
  }
  
// called when the window is scrolled.  
  var scroll = $(window).scrollTop();
  if(scroll >= 420){
   $(".custom-sidebar1").addClass("sticky-fix");     
  }else{
    $(".custom-sidebar1").removeClass("sticky-fix"); 
  }
  
  if(h1 >= h2) {
//       $(".custom-sidebar").addClass("sticky-fix-bottom");
  }else{
    $(".custom-sidebar1").css("top", scroll+"px");
//     $(".custom-sidebar").removeClass("sticky-fix-bottom");
  }
//   $(".custom-sidebar").css("top", scroll+"px");
  
 
} 
 

   </script>
