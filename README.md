import random
import statistics
import numpy as np
List = [x for x in range (80,120)]

def get_value(signal,deviation):
    deviation_magnitude = deviation * signal
    value = random.uniform(signal - deviation_magnitude, signal + deviation_magnitude)
    return value

a_payoff = []
b_payoff = []
c_payoff = []
d_payoff = []
e_payoff = []

no_simulations = int(input("Enter the number of times you want the game to run: "))
for i in range (no_simulations):

    a_win_count = 0
    b_win_count = 0
    c_win_count = 0
    d_win_count = 0
    e_win_count = 0

    highest_losing_list = []

    player_a_signal = random.choice(List) + random.random()
    player_b_signal = random.choice(List) + random.random()
    player_c_signal = random.choice(List) + random.random()
    player_d_signal = random.choice(List) + random.random()
    player_e_signal = random.choice(List) + random.random()

    winners_list = []

    for k in range(5):

        value_a = get_value(player_a_signal,0.02)
        value_b = get_value(player_b_signal,0.05)
        value_c = get_value(player_c_signal,0.1)
        value_d = get_value(player_d_signal,0.15)
        value_e = get_value(player_e_signal,0.20)

        values_list = [value_a,value_b,value_c,value_d,value_e]

        max_bid = max(values_list)
        for j in range (5):
            if max_bid == values_list[j]:
                max_bid_index = j
        values_list.pop(j)
        highest_losing_bid = max(values_list)
        highest_losing_list.append(highest_losing_bid)
        if max_bid == value_a :
            a_win_count = a_win_count + 1
            #a_win_payoff.append(player_a_signal - highest_losing_bid)

        if max_bid == value_b :
            b_win_count = b_win_count + 1
            #b_win_payoff.append(player_b_signal - highest_losing_bid)

        if max_bid == value_c :
            c_win_count = c_win_count + 1
            #c_win_payoff.append(player_c_signal - highest_losing_bid)

        if max_bid == value_d :
            d_win_count = d_win_count + 1
            #d_win_payoff.append(player_d_signal - highest_losing_bid)

        if max_bid == value_e :
            e_win_count = e_win_count + 1
            #e_win_payoff.append(player_e_signal - highest_losing_bid)
    
    win_count_list = [a_win_count,b_win_count,c_win_count,d_win_count,e_win_count]
    if a_win_count == max(win_count_list):
        winners_list.append("a")
    if b_win_count == max(win_count_list):
        winners_list.append("b")
    if c_win_count == max(win_count_list):
        winners_list.append("c")
    if d_win_count == max(win_count_list):
        winners_list.append("d")
    if e_win_count == max(win_count_list):
        winners_list.append("e")
    winner = random.choice(winners_list)
    #squared_list = np.square(highest_losing_list)
    #mean_squared = np.mean(squared_list)
    rms = np.average(highest_losing_list)
    if winner == "a":
        a_payoff.append(player_a_signal - rms)
    if winner == "b":
        b_payoff.append(player_b_signal - rms)
    if winner == "c":
        c_payoff.append(player_c_signal - rms)
    if winner == "d":
        d_payoff.append(player_d_signal - rms)
    if winner == "e":
        e_payoff.append(player_e_signal - rms)
    
a_average_payoff = np.average(a_payoff)
b_average_payoff = np.average(b_payoff)
c_average_payoff = np.average(c_payoff)
d_average_payoff = np.average(d_payoff)
e_average_payoff = np.average(e_payoff)
average_payoff_list = [a_average_payoff,b_average_payoff,c_average_payoff,d_average_payoff,e_average_payoff]



print("the average payoff for the player with deviation 2% is",average_payoff_list[0])
print("the average payoff for the player with deviation 5% is",average_payoff_list[1])
print("the average payoff for the player with deviation 10% is",average_payoff_list[2])
print("the average payoff for the player with deviation 15% is",average_payoff_list[3])
