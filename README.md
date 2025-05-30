# Indian_Election_Analysis

## Project Overview

This project analyzes the results of the India General Election 2024 using SQL Server. Various problem statements were tackled to gain insights from the election data. Dataset contains the election result of India consisting of 5 different database, each database having different information of the election result of India.

## ER Diagram
![ER Diagram](https://github.com/user-attachments/assets/96403344-d4e7-4bf9-a268-36ae7bd8e071)

## Problem Statement & Solutions

### Problem 1: Total Seats
Question: Determine the total number of parliamentary constituencies.

Query:

    SELECT distinct
        COUNT(Parliament_Constituency) as total_Seats
    FROM
        constituencywise_results;


### Problem statement-2: What is the total number of seats available for elections in each state 
Question:
Determine the total number of parliamentary seats available per state.

Query:

    SELECT
        s.State as STATE_NAME,
        COUNT(sr.Parliament_Constituency) as TOTAL_SEATS_BY_EACH_STATE
    FROM
        statewise_results sr
        INNER JOIN states s ON s.State_ID = sr.State_ID
    GROUP BY
        s.State

### Problem statement-3: What is the total number of seats available for elections in each state by assending order
Question: Determine the total seats per state, sorted in ascending order.

Query:

    SELECT
        s.State AS STATE_NAME,
        COUNT(sr.Parliament_Constituency) AS TOTAL_SEATS_BY_EACH_STATE
    FROM
        statewise_results sr
        INNER JOIN states s ON s.State_ID = sr.State_ID
    GROUP BY
        s.State
    ORDER BY
        TOTAL_SEATS_BY_EACH_STATE asc;

### Problem statement-4: What is the total number of seats available for elections in each state by descending order 
Question: Determine the total seats per state, sorted in descending order.

Query:

    SELECT
        s.State AS STATE_NAME,
        COUNT(sr.Parliament_Constituency) AS TOTAL_SEATS_BY_EACH_STATE
    FROM
        statewise_results sr
        INNER JOIN states s ON s.State_ID = sr.State_ID
    GROUP BY
        s.State
    ORDER BY
        TOTAL_SEATS_BY_EACH_STATE DESC;
        
### Problem statement-5: Total Seats Won by NDA Allianz
Question: Calculate the total seats won by NDA alliance parties.

Query:

    SELECT 
        SUM(CASE 
                WHEN party IN (
                    'Bharatiya Janata Party - BJP', 
                    'Telugu Desam - TDP', 
				      'Janata Dal  (United) - JD(U)',
                    'Shiv Sena - SHS', 
                    'AJSU Party - AJSUP', 
                    'Apna Dal (Soneylal) - ADAL', 
                    'Asom Gana Parishad - AGP',
                    'Hindustani Awam Morcha (Secular) - HAMS', 
                    'Janasena Party - JnP', 
				      'Janata Dal  (Secular) - JD(S)',
                    'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                    'Nationalist Congress Party - NCP',
                    'Rashtriya Lok Dal - RLD', 
                    'Sikkim Krantikari Morcha - SKM'
                ) THEN [Won]
                ELSE 0 
            END) AS NDA_Total_Seats_Won
    FROM 
        partywise_results;

### Problem statement-6: Seats Won by NDA Allianz Parties 
Question: Retrieve the seats won by each NDA alliance party.

Query:

    SELECT 
        party as Party_Name,
        won as Seats_Won
    FROM 
        partywise_results
    WHERE 
        party IN (
            'Bharatiya Janata Party - BJP', 
            'Telugu Desam - TDP', 
    		'Janata Dal  (United) - JD(U)',
            'Shiv Sena - SHS', 
            'AJSU Party - AJSUP', 
            'Apna Dal (Soneylal) - ADAL', 
            'Asom Gana Parishad - AGP',
            'Hindustani Awam Morcha (Secular) - HAMS', 
            'Janasena Party - JnP', 
    		'Janata Dal  (Secular) - JD(S)',
            'Lok Janshakti Party(Ram Vilas) - LJPRV', 
            'Nationalist Congress Party - NCP',
            'Rashtriya Lok Dal - RLD', 
            'Sikkim Krantikari Morcha - SKM'
        )
    ORDER BY Seats_Won DESC;

### Problem statement-7: Total Seats Won by I.N.D.I.A. Allianz
Question: The objective of this query is to calculate the total number of parliamentary seats secured by all political parties that are part of the I.N.D.I.A.

Query:

    SELECT 
        SUM(CASE 
                WHEN party IN (
                    'Indian National Congress - INC',
                    'Aam Aadmi Party - AAAP',
                    'All India Trinamool Congress - AITC',
                    'Bharat Adivasi Party - BHRTADVSIP',
                    'Communist Party of India  (Marxist) - CPI(M)',
                    'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                    'Communist Party of India - CPI',
                    'Dravida Munnetra Kazhagam - DMK',
                    'Indian Union Muslim League - IUML',
                    'Nat`Jammu & Kashmir National Conference - JKN',
                    'Jharkhand Mukti Morcha - JMM',
                    'Jammu & Kashmir National Conference - JKN',
                    'Kerala Congress - KEC',
                    'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                    'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                    'Rashtriya Janata Dal - RJD',
                    'Rashtriya Loktantrik Party - RLTP',
                    'Revolutionary Socialist Party - RSP',
                    'Samajwadi Party - SP',
                    'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                    'Viduthalai Chiruthaigal Katchi - VCK'
                ) THEN [Won]
                ELSE 0 
            END) AS INDIA_Total_Seats_Won
    FROM 
        partywise_results

### Problem statement-8: Seats Won by I.N.D.I.A. Allianz Parties
Question: The goal of this query is to list the number of seats won by each political party that is part of the I.N.D.I.A. (Indian National Developmental Inclusive Alliance). 

Query:

    SELECT 
        party as Party_Name,
        won as Seats_Won
    FROM 
        partywise_results
    WHERE 
        party IN (
            'Indian National Congress - INC',
                    'Aam Aadmi Party - AAAP',
                    'All India Trinamool Congress - AITC',
                    'Bharat Adivasi Party - BHRTADVSIP',
                    'Communist Party of India  (Marxist) - CPI(M)',
                    'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                    'Communist Party of India - CPI',
                    'Dravida Munnetra Kazhagam - DMK',
                    'Indian Union Muslim League - IUML',
                    'Nat`Jammu & Kashmir National Conference - JKN',
                    'Jharkhand Mukti Morcha - JMM',
                    'Jammu & Kashmir National Conference - JKN',
                    'Kerala Congress - KEC',
                    'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                    'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                    'Rashtriya Janata Dal - RJD',
                    'Rashtriya Loktantrik Party - RLTP',
                    'Revolutionary Socialist Party - RSP',
                    'Samajwadi Party - SP',
                    'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                    'Viduthalai Chiruthaigal Katchi - VCK'
        )
    ORDER BY Seats_Won DESC

### Problem statement-9:  Add new column field in table partywise_results to get the Party Allianz as NDA, I.N.D.I.A and OTHER 
Question:

Query:

    ALTER TABLE partywise_results
    ADD party_alliance VARCHAR(50);
I.N.D.I.A Allianz

    UPDATE partywise_results
    SET party_alliance = 'I.N.D.I.A'
    WHERE party IN (
        'Indian National Congress - INC',
        'Aam Aadmi Party - AAAP',
        'All India Trinamool Congress - AITC',
        'Bharat Adivasi Party - BHRTADVSIP',
        'Communist Party of India  (Marxist) - CPI(M)',
        'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
        'Communist Party of India - CPI',
        'Dravida Munnetra Kazhagam - DMK',	
        'Indian Union Muslim League - IUML',
        'Jammu & Kashmir National Conference - JKN',
        'Jharkhand Mukti Morcha - JMM',
        'Kerala Congress - KEC',
        'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
        'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
        'Rashtriya Janata Dal - RJD',
        'Rashtriya Loktantrik Party - RLTP',
        'Revolutionary Socialist Party - RSP',
        'Samajwadi Party - SP',
        'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
        'Viduthalai Chiruthaigal Katchi - VCK'
    );
    
NDA Allianz

    UPDATE partywise_results
    SET party_alliance = 'NDA'
    WHERE party IN (
        'Bharatiya Janata Party - BJP',
        'Telugu Desam - TDP',
        'Janata Dal  (United) - JD(U)',
        'Shiv Sena - SHS',
        'AJSU Party - AJSUP',
        'Apna Dal (Soneylal) - ADAL',
        'Asom Gana Parishad - AGP',
        'Hindustani Awam Morcha (Secular) - HAMS',
        'Janasena Party - JnP',
        'Janata Dal  (Secular) - JD(S)',
        'Lok Janshakti Party(Ram Vilas) - LJPRV',
        'Nationalist Congress Party - NCP',
        'Rashtriya Lok Dal - RLD',
        'Sikkim Krantikari Morcha - SKM'
    );
    
OTHER

    UPDATE partywise_results
    SET party_alliance = 'OTHER'
    WHERE party_alliance IS NULL;

### Problem statement-10:  Which party alliance (NDA, I.N.D.I.A, or OTHER) won the most seats across all states?
Query:

    SELECT 
        p.party_alliance,
        COUNT(cr.Constituency_ID) AS Seats_Won
    FROM 
        constituencywise_results cr
    JOIN 
        partywise_results p ON cr.Party_ID = p.Party_ID
    WHERE 
        p.party_alliance IN ('NDA', 'I.N.D.I.A', 'OTHER')
    GROUP BY 
        p.party_alliance
    ORDER BY 
        Seats_Won DESC;

### Problem statement-11:  Winning candidate's name, their party name, total votes, and the margin of victory for a specific state and constituency?
Query:

    SELECT cr.Winning_Candidate, p.Party, p.party_alliance, cr.Total_Votes, cr.Margin, cr.Constituency_Name, s.State
    FROM constituencywise_results cr
    JOIN partywise_results p ON cr.Party_ID = p.Party_ID
    JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
    JOIN states s ON sr.State_ID = s.State_ID
    WHERE s.State = 'Uttar Pradesh' AND cr.Constituency_Name = 'AMETHI';
    
### Problem statement-12:  What is the distribution of EVM votes versus postal votes for candidates in a specific constituency?
Query:

    SELECT 
        cd.Candidate,
        cd.Party,
        cd.EVM_Votes,
        cd.Postal_Votes,
        cd.Total_Votes,
        cr.Constituency_Name
    FROM 
        constituencywise_details cd
    JOIN 
        constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
    WHERE 
        cr.Constituency_Name = 'MATHURA'
    ORDER BY cd.Total_Votes DESC;

### Problem statement-13:  Which parties won the most seats in s State, and how many seats did each party win?
Query:

    SELECT 
        p.Party,
        COUNT(cr.Constituency_ID) AS Seats_Won
    FROM 
        constituencywise_results cr
    JOIN 
        partywise_results p ON cr.Party_ID = p.Party_ID
    JOIN 
        statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
    JOIN states s ON sr.State_ID = s.State_ID
    WHERE 
        s.state = 'Andhra Pradesh'
    GROUP BY 
        p.Party
    ORDER BY 
        Seats_Won DESC;

### Problem statement-14:  What is the total number of seats won by each party alliance (NDA, I.N.D.I.A, and OTHER) in each state for the India Elections 2024
Query:

    SELECT 
        s.State AS State_Name,
        SUM(CASE WHEN p.party_alliance = 'NDA' THEN 1 ELSE 0 END) AS NDA_Seats_Won,
        SUM(CASE WHEN p.party_alliance = 'I.N.D.I.A' THEN 1 ELSE 0 END) AS INDIA_Seats_Won,
    	SUM(CASE WHEN p.party_alliance = 'OTHER' THEN 1 ELSE 0 END) AS OTHER_Seats_Won
    FROM 
        constituencywise_results cr
    JOIN 
        partywise_results p ON cr.Party_ID = p.Party_ID
    JOIN 
        statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
    JOIN 
        states s ON sr.State_ID = s.State_ID
    WHERE 
        p.party_alliance IN ('NDA', 'I.N.D.I.A',  'OTHER')  -- Filter for NDA and INDIA alliances
    GROUP BY 
        s.State
    ORDER BY 
        s.State;

### Problem statement-15:  Which candidate received the highest number of EVM votes in each constituency (Top 10)?
Query:

    SELECT TOP 10
        cr.Constituency_Name,
        cd.Constituency_ID,
        cd.Candidate,
        cd.EVM_Votes
    FROM 
        constituencywise_details cd
    JOIN 
        constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
    WHERE 
        cd.EVM_Votes = (
            SELECT MAX(cd1.EVM_Votes)
            FROM constituencywise_details cd1
            WHERE cd1.Constituency_ID = cd.Constituency_ID
        )
    ORDER BY 
        cd.EVM_Votes DESC;

### Problem statement-16:  Which candidate won and which candidate was the runner-up in each constituency of State for the 2024 elections?
Query:

    WITH RankedCandidates AS (
        SELECT 
            cd.Constituency_ID,
            cd.Candidate,
            cd.Party,
            cd.EVM_Votes,
            cd.Postal_Votes,
            cd.EVM_Votes + cd.Postal_Votes AS Total_Votes,
            ROW_NUMBER() OVER (PARTITION BY cd.Constituency_ID ORDER BY cd.EVM_Votes + cd.Postal_Votes DESC) AS VoteRank
        FROM 
            constituencywise_details cd
        JOIN 
            constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
        JOIN 
            statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
        JOIN 
            states s ON sr.State_ID = s.State_ID
        WHERE 
            s.State = 'Maharashtra'
    )
    
    SELECT 
        cr.Constituency_Name,
        MAX(CASE WHEN rc.VoteRank = 1 THEN rc.Candidate END) AS Winning_Candidate,
        MAX(CASE WHEN rc.VoteRank = 2 THEN rc.Candidate END) AS Runnerup_Candidate
    FROM 
        RankedCandidates rc
    JOIN 
        constituencywise_results cr ON rc.Constituency_ID = cr.Constituency_ID
    GROUP BY 
        cr.Constituency_Name
    ORDER BY 
        cr.Constituency_Name;

### Problem statement-17:  For the state of Maharashtra, what are the total number of seats, total number of candidates, total number of parties, total votes (including EVM and postal), and the breakdown of EVM and postal votes?
Query:

    SELECT 
        COUNT(DISTINCT cr.Constituency_ID) AS Total_Seats,
        COUNT(DISTINCT cd.Candidate) AS Total_Candidates,
        COUNT(DISTINCT p.Party) AS Total_Parties,
        SUM(cd.EVM_Votes + cd.Postal_Votes) AS Total_Votes,
        SUM(cd.EVM_Votes) AS Total_EVM_Votes,
        SUM(cd.Postal_Votes) AS Total_Postal_Votes
    FROM 
        constituencywise_results cr
    JOIN 
        constituencywise_details cd ON cr.Constituency_ID = cd.Constituency_ID
    JOIN 
        statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
    JOIN 
        states s ON sr.State_ID = s.State_ID
    JOIN 
        partywise_results p ON cr.Party_ID = p.Party_ID
    WHERE 
        s.State = 'Maharashtra';
