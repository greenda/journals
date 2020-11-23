<script>
	import * as data from './journal.json';
	import Article from './Article/Article.svelte';
    import JournalNavigation from './JournalNavigation/JournalNavigation.svelte';

	let elements = {};

	let isJournalNavPanelHidden = true;

	const focusArticle = id => {
		console.log('focusArticle ' + id + ' ' + elements[id]);	
		elements[id].scrollIntoView();
	}

	const setArticleRef = (id, ref) => elements[id] = ref;

	const toggleJournalNavPanel = () => {
		console.log('toggleJournalNavPanel')
		isJournalNavPanelHidden = !isJournalNavPanelHidden;
	}
</script>

<style>
.main {
    display: grid;
    grid-template-areas:
        /* "left-header header right-header" */
        "nav article ads"
        "footer footer footer";
    grid-template-rows: 1fr 8px;
    grid-template-columns: 1fr 800px 1fr;
    height: auto;
    font-family: fell, Georgia, Cambria, "Times New Roman", Times, serif;
    font-weight: 400;
    letter-spacing: -0.003em;
    line-height: 32px;
    font-size: 21px;
    background: #a2b9bc;
}

@media (max-width: 800px) {
    .main {
        padding-top: 20px;
        grid-template-rows: 1fr 8px;
        grid-template-columns: 20px 1fr 20px;
    }

    .siteAds__button-hidden {
        display: none;
    }
}

.footer {
    grid-area: footer;
    margin: 8px;
    padding: 8px;
}

.mainArticle {
    grid-area: article;
    padding: 0 32px;
    box-shadow: 0px 0 10px rgba(0,0,0,0.7);    	
    background: white;
    z-index: 1;
}

.mainNav {
    grid-area: nav;
    padding: 20px;	
}

.siteAds {
    grid-area: ads;
    line-height: normal;
}

.siteAds__content {
    position: sticky;
    top: 60px; 
    padding: 8px;
}

.siteAds__shown {
    background: white;
    box-shadow: 0px 0 10px rgba(0,0,0,0.7);
    text-align: right; 
    padding: 8px;
    z-index: 1;
    max-width: 180px;
}

.siteAds__hidden {
    background: inherit;
    padding: 8px;
}

.siteAds__hidden > .siteAds__content {
    display: none;
}

.siteAds > button {
    position: sticky;
    top: 8px; 
    width: 42px;
    font-weight: bold;    
}

.siteAds__button-hidden {
    border: none;
}

.siteAds__button-hidden::before {
    content: ">";		
}

.siteAds__button-hidden::before {
    content: ">";
}

.siteAds__button-shown::before {
    content: "<";
}

.journalTitle {
    width: auto;
    text-align: center;
}

.epigraph {
    width: auto;
    text-align: right;
    line-height: 16px;
    font-style: italic;
    margin-bottom: 32px;
}

.epigraph__annotation {
    margin-top: 8px;
    font-size: 0.8em;
}
</style>

<body class="main">
	<article class="mainArticle">
		<div class="journalTitle">
			<h2>{data.title}</h2>
		</div>
		
		
		{#each data.epigraphes as epigraph}
			<div class="epigraph">
				{#each epigraph.paragraphes as paragraph}
					<p>{paragraph}</p>	
				{/each}	
				<p class="epigraph__annotation">{epigraph.annotation}</p>		
			</div>
		{/each}
		
		{#each data.articles as article}
			<Article
				{article}
				onMount={setArticleRef}
			/>
		{/each}
	</article>
	<nav class="mainNav"></nav>
	<div class={isJournalNavPanelHidden ? 'siteAds siteAds__hidden' : 'siteAds siteAds__shown'}>
		<button class={isJournalNavPanelHidden ? 'siteAds__button-hidden' : 'siteAds__button-shown'} on:click={toggleJournalNavPanel}></button>
		<div class="siteAds__content">
			<JournalNavigation articles={data.articles} onSelect={focusArticle}/>
		</div>		
	</div>
	<footer class="footer"></footer>
</body>