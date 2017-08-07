---
layout: project

# Global
meta:
  title: Red Finch Perch Add-ons | PHP, Open Source, Perch CMS | James Wigger, Web Developer
  description: Case study of my own source applications for the Perch content management system.

# Page
title: Red Finch Add-ons
type: Open Source
thumbnail: /assets/resources/red-finch/thumbnail.png
intro: Giving back to the community here are a series of Perch add-ons that extend the functionality of the CMS and aim to solve real world problems for end-users and developers alike.
website: https://github.com/redfinch
---

<section class="c-section">
	<div class="o-container">
		
		<div class="o-media">
			<div class="o-media__object" data-scroll>
				<figure class="c-card">
				    <img src="/assets/resources/red-finch/red-finch-logo.png" srcset="/assets/resources/red-finch/red-finch-logo@2x.png 2x" alt="Red Finch bird logo" />
				</figure>
			</div>
			<div class="o-media__article">
				
				<div class="o-content">
					<div class="o-content__header">
					
			            <header class="c-header">
                            <h1 class="c-header__title">
                                Red Finch
                            </h1>
                        </header>
                        
					</div>
					<div class="o-content__main is-raw">
					    <p>
					        The idea behind Red Finch is to provide a more recognisable name under which to release my open source Perch add-ons. 
					        It provides scope for future contributors much in the same way as the League of Packages. The core ethos is 
					        that all add-ons should be free, simple and fulfil a specific task that Perch alone cannot accomplish. The logo and
					        colours were a fun excersise in developing a brand from scratch.
					    </p>
					</div>
				</div>
				
			</div>
		</div>
		
	</div>
</section>

<section class="c-section c-section--alt">
	<div class="o-container">
	
		<figure class="c-card u-m-btm" data-scroll>
            <img src="/assets/resources/red-finch/events-list.png" alt="Index page of the event logger listing recent activity" />
        </figure>
        
        <div class="o-single u-align-center">
        
	        <div class="o-content">
				<div class="o-content__header">
				
		            <header class="c-header c-header--center">
	                    <h1 class="c-header__title">
	                        Event Logger
	                    </h1>
	                </header>
	                
				</div>
				<div class="o-content__main is-raw">
				    <p>
				        Building on one of my more popular add-ons the event logger provides a running list of user activity within Perch.
				    </p>
				    <p>
				        Using the built in events API, the system provides an abstraction layer that means the diverse events (from uploading images, to editing a category name)
				        as well as handling the customisable templates produced by developers are transformed into a standard format for logging.
				    </p>
				    <p>
				        For a more detailed write-up of the goals and decisions (including code examples) <a href="/blog/the-red-finch-event-logger.html">see my blog post here</a>.
				    </p>
				</div>
			</div>
        
        </div>
	
	</div>
</section>

<section class="c-section">
	<div class="o-container">
	    
        <div class="o-double">
        
            <div class="o-double__item">
                <figure class="c-card u-m-btm" data-scroll>
                    <img src="/assets/resources/red-finch/events-view.png" alt="Zoomed view of the code viewer within an event" />
                </figure>
	            <div class="o-content">
					<div class="o-content__header">
					
		                <header class="c-header c-header--sm">
	                        <h1 class="c-header__title">
	                            A deep dive into content changes
	                        </h1>
	                    </header>
	                    
					</div>
					<div class="o-content__main is-raw">
					    <p>
					        The event detail view provides a clean way of showing content changes. The user, event type and other 
					        meta data is displayed clearly at the top while the template updates are shown in full below. A syntax highlighter
					        is used to help non-developers to see the written content.
					    </p>
					</div>
				</div>
			</div>
			
            <div class="o-double__item">
                <figure class="c-card u-m-btm" data-scroll>
                    <img src="/assets/resources/red-finch/events-history.png" alt="Example of the history view showing differences between events" />
                </figure>
                <div class="o-content">
                    <div class="o-content__header">
                    
                        <header class="c-header c-header--sm">
                            <h1 class="c-header__title">
                                A look back in time
                            </h1>
                        </header>
                        
                    </div>
                    <div class="o-content__main is-raw">
                        <p>
                            A history view tracks changes over time, giving editors a great insight into how the content has evolved.
                            For auditing purposes it can reveal when a certain item has been added to a page and by who.
                        </p>
                    </div>
                </div>
            </div>
        
        </div>
	
	</div>
</section>

<section class="c-section c-section--alt">
	<div class="o-container">
	
		<figure class="c-card u-m-btm" data-scroll>
            <img src="/assets/resources/red-finch/optimiser-tasks.png" alt="List of optimisation tasks that have been completed" />
        </figure>
        
        <div class="o-single u-align-center">
        
	        <div class="o-content">
				<div class="o-content__header">
				
		            <header class="c-header c-header--center">
	                    <h1 class="c-header__title">
	                        Image Optimiser
	                    </h1>
	                </header>
	                
				</div>
				<div class="o-content__main is-raw">
				    <p>
				        The image optimiser was developed to solve the problem of compression user uploaded images 
				        using open source software (jpegoptim, optipng, gifsicle) and a scheduled task system to 
				        track uploaded images and compress them.
				    </p>
				    <p>
				       Developers can configure the compression levels within the CMS interface and the entire experience
				       is hidden from end-users - meeting a key development goal.
				    </p>
				    <p>
				        For a more in-depth article <a href="/blog/automatic-image-optimisation-for-perch-cms.html">see my post here</a>.
				    </p>
				</div>
			</div>
        
        </div>
	
	</div>
</section>

<section class="c-section">
	<div class="o-container">
	    
        <div class="o-double">
        
            <div class="o-double__item">
                <figure class="c-card u-m-btm" data-scroll>
                    <img src="/assets/resources/red-finch/optimiser-scheduled.png" alt="List of the scheduled task operations showing successes and warnings" />
                </figure>
	            <div class="o-content">
					<div class="o-content__header">
					
		                <header class="c-header c-header--sm">
	                        <h1 class="c-header__title">
	                            Performance through-and-through
	                        </h1>
	                    </header>
	                    
					</div>
					<div class="o-content__main is-raw">
					    <p>
					        An app focused on optimisation should not affect a user's workflow. All image uploads are tracked
					        using the native Perch events system and scheduled for later processing. Garbage collection tasks prevent the UI
					        from being cluttered with completed tasks.
					    </p>
					</div>
				</div>
			</div>
			
            <div class="o-double__item">
                <figure class="c-card u-m-btm" data-scroll>
                    <img src="/assets/resources/red-finch/optimiser-settings.png" alt="Zoomed in view of the options for jpegoptim" />
                </figure>
                <div class="o-content">
                    <div class="o-content__header">
                    
                        <header class="c-header c-header--sm">
                            <h1 class="c-header__title">
                                Fully configurable
                            </h1>
                        </header>
                        
                    </div>
                    <div class="o-content__main is-raw">
                        <p>
                            Those granted access can completely customise how optimisation occurs. 
                            Tools can be toggled and the level of compression can be set individually between image types. These options are passed through to
                            the underlying system libraries.
                        </p>
                    </div>
                </div>
            </div>
        
        </div>
	
	</div>
</section>

<section class="c-section c-section--alt">
	<div class="o-container">
	
		<figure class="c-card u-m-btm" data-scroll>
            <img src="/assets/resources/red-finch/red-finch-homepage.jpg" alt="Full screen view of the Red Finch home page" />
        </figure>
        
        <div class="o-single u-align-center">
        
	        <div class="o-content">
				<div class="o-content__header">
				
		            <header class="c-header c-header--center">
	                    <h1 class="c-header__title">
	                        Providing Documentation
	                    </h1>
	                </header>
	                
				</div>
				<div class="o-content__main is-raw">
				    <p>
				        It is a personal belief that all released software should come with documentation. With my own add-ons
				        I took the opportunity to build a dedicated page listing available releases and providing plenty
				        of information to get other developers started.
				    </p>
				    <p>
				       The page is built on Jekyll and GitHub pages, with the design being built using the Bulma CSS framework.
				    </p>
				</div>
			</div>
        
        </div>
	
	</div>
</section>
