# Dining Philosophers – Fork Assignment Demo

This is a simple visual and code explanation for the classic **Dining Philosophers** problem, focused on how forks are assigned to each philosopher to avoid deadlock.

## Function used in C

The main function for assigning forks is:

```c
/**
 * philo_id != relative position in the array 
 * (we start by 0 and the first philo is id 1)
 * Right fork -> Position of the fork
 * Left fork is more tricky:
 * - For example, the LEFT FORK of philosopher 5 (position 4) is 0:
 *   left_fork = (philo_pos + 1) % philo_nbr; // (4 + 1) % 5 = 0
 * Each philosopher needs 2 forks to eat.
 * To prevent deadlock:
 *   - If philosopher is even: takes right fork first, then left.
 *   - If philosopher is odd: takes left fork first, then right.
 */
static void assign_forks(t_philo *philo, t_fork *forks, int philo_position)
{
    int philo_nbr = philo->table->philo_nbr;
    philo->first_fork  = &forks[(philo_position + 1) % philo_nbr];
    philo->second_fork = &forks[philo_position];
    if (philo->id % 2 == 0)
    {
        philo->first_fork  = &forks[philo_position];
        philo->second_fork = &forks[(philo_position + 1) % philo_nbr];
    }
}
```

## How it works

- There are `N` philosophers sitting around a table, each with a plate and a fork between them.
- Each philosopher needs **two forks** to eat: one on the left, one on the right.
- To avoid deadlock (everyone waiting forever).

## Example

With 5 philosophers:
- Philosopher 5 (position 4):  
  - Left fork = (4+1)%5 = 0  
  - Right fork = 4

## Note

I'm a student, so if something is wrong or not clear, sorry!  
Just trying to understand and visualize this classic concurrency problem.
