<script>
    import Card from "./Card.svelte";
    import Filter from "./Filter.svelte";
    let companies = [
        {
            name: "Photosnap",
            jobTitle: "Senior Frontend Developer",
            postTime: "1d ago",
            jobStatus: "Full Time",
            location: "USA only",
            keyWords: ["Frontend", "Senior", "HTML", "CSS", "JavaScript"],
            isNew: true,
            featured: true,
            logoUrl: "images/photosnap.svg",
        },
        {
            name: "Manage",
            jobTitle: "Fullstack Developer",
            postTime: "1d ago",
            jobStatus: "Part Time",
            location: "Remote",
            keyWords: ["Fullstack", "Midweight", "Python", "React"],
            isNew: true,
            featured: true,
            logoUrl: "images/manage.svg",
        },
        {
            name: "Account",
            jobTitle: "Junior Frontend Developer",
            postTime: "2d ago",
            jobStatus: "Part Time",
            location: "USA only",
            keyWords: ["Frontend", "Junior", "React", "Sass", "JavaScript"],
            isNew: true,
            featured: false,
            logoUrl: "images/account.svg",
        },
        {
            name: "MyHome",
            jobTitle: "Junior Frontend Developer",
            postTime: "5d ago",
            jobStatus: "Contract",
            location: "USA only",
            keyWords: ["Frontend", "Junior", "CSS", "JavaScript"],
            isNew: false,
            featured: false,
            logoUrl: "images/myhome.svg",
        },
        {
            name: "Loop Studios",
            jobTitle: "Software Engineer",
            postTime: "1w ago",
            jobStatus: "Full Time",
            location: "Worldwide",
            keyWords: ["Fullstack", "Midweight", "JavaScript", "SASS", "Ruby"],
            isNew: false,
            featured: false,
            logoUrl: "images/loop-studios.svg",
        },
        {
            name: "FaceIt",
            jobTitle: "Junior Backend Developer",
            postTime: "2w ago",
            jobStatus: "Full Time",
            location: "UK only",
            keyWords: ["Backend", "Junior", "Ruby", "RoR"],
            isNew: false,
            featured: false,
            logoUrl: "images/faceit.svg",
        },
        {
            name: "Shortly",
            jobTitle: "Junior Developer",
            postTime: "2w ago",
            jobStatus: "Full Time",
            location: "Worldwide",
            keyWords: ["Frontend", "Junior", "HTML", "SASS", "JavaScript"],
            isNew: false,
            featured: false,
            logoUrl: "images/shortly.svg",
        },
        {
            name: "Insure",
            jobTitle: "Junior Developer",
            postTime: "2w ago",
            jobStatus: "Full Time",
            location: "USA only",
            keyWords: ["Frontend", "Junior", "Vue", "JavaScript", "Sass"],
            isNew: false,
            featured: false,
            logoUrl: "images/insure.svg",
        },
        {
            name: "Eyecam Co.",
            jobTitle: "Junior Developer",
            postTime: "3w ago",
            jobStatus: "Full Time",
            location: "Worldwide",
            keyWords: [
                "Fullstack",
                "Midweight",
                "JavaScript",
                "Django",
                "Python",
            ],
            isNew: false,
            featured: false,
            logoUrl: "images/eyecam-co.svg",
        },
        {
            name: "The Air Filter Company",
            jobTitle: "Front-end Dev",
            postTime: "1mo ago",
            jobStatus: "Full Time",
            location: "Worldwide",
            keyWords: ["Frontend", "Junior", "React", "Sass", "JavaScript"],
            isNew: false,
            featured: false,
            logoUrl: "images/the-air-filter-company.svg",
        },
    ];
    let displayCompany = companies;
    var filter_keywords = [];
    function handleAddKeyword(event) {
        pushOnly(event.detail.text.keyword);
        filterCompanyWithKeyword();
    }
    function filterCompanyWithKeyword(){
        displayCompany = [];
        companies.forEach(comp=>{
            if(filter_keywords.every(val=>comp.keyWords.includes(val))){
                displayCompany.push(comp);
            }
        });
        displayCompany = displayCompany;
    }
    function pushOnly(word){
        if(filter_keywords.includes(word)){
            return;
        }else{
            filter_keywords.push(word);
            filter_keywords = filter_keywords;
        }
    }
    function handleRemoveKeyword(event){
        filter_keywords = filter_keywords.filter(e=> e!== event.detail);
        filterCompanyWithKeyword();
    }
    function handleClear(){
        filter_keywords = [];
        displayCompany = companies;
    }
</script>

<style>
    .cards-container {
        background-color: #effafa;
        padding: 56px 2rem 2rem 1.5rem;
    }
    .hasKeyword{
        padding: 1.4rem 2rem 2rem 1.5rem !important;
    }
    @media (min-width: 1200px) {
        .cards-container {
            min-height: 100vh;
            padding: 76px 128px 2rem 128px;
        }
        .hasKeyword{
            padding: 1rem 128px 2rem 128px !important;
        }
        
    }
</style>

<div class="container cards-container" class:hasKeyword="{filter_keywords.length>0}">
    <Filter words={filter_keywords} on:removeKeyword={handleRemoveKeyword} on:clearKeyword={handleClear}/>
    {#each displayCompany as company}
        <Card {...company} on:message={handleAddKeyword} />
    {/each}
</div>
<!-- {
    name:"",
    jobtitle:"",
    post-time:"",
}, -->
