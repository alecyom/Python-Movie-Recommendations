import requests
import json

def get_movies_from_tastedive(movie_name):
    tastedive = "https://tastedive.com/api/similar"
    params_diction = {}
    params_diction['q'] = movie_name
    params_diction['type'] = 'movies'
    params_diction['limit'] = 5

    movie = requests.get(tastedive, params = params_diction)
   
    print(movie.url)
    return movie.json()

def extract_movie_titles(movie):
    title_lst = [name["Name"]for name in movie["Similar"]["Results"]]
    return title_lst

def get_related_titles(movie_lst):
    title_lst = []
    for movie in movie_lst:
        get_movie = get_movies_from_tastedive(movie)
        extracted_movies = extract_movie_titles(get_movie)
        for movie_title in extracted_movies:
            if movie_title not in title_lst:
                title_lst.append(movie_title)
    return title_lst

def get_movie_data(movie_name):
    OMDB = "http://www.omdbapi.com/"
    params_diction = {}
    params_diction['t'] = movie_name
    params_diction['r'] = 'json'
  
    movie_data = requests_with_caching.get(OMDB, params = params_diction)
   
    print(movie_data.url)
    return movie_data.json()

def get_movie_rating(movie_data):
    for rate in movie_data['Ratings']:
        if rate['Source'] == 'Rotten Tomatoes':
            return int(rate['Value'][:2])
    return int(0)

def get_sorted_recommendations(input_movie):
    recommended = []
    related = get_related_titles(input_movie)
    for movie in related:
        recommended.append(movie)
           
    sorted_recommendations = sorted(recommended, key = lambda x: (get_movie_rating(get_movie_data(x)), x), reverse = True)
 
    return sorted_recommendations
