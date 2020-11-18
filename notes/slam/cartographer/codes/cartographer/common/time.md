cartographer/common/time.h

```
struct UniversalTimeScaleClock {
  using rep = int64;
  using period = std::ratio<1, 10000000>;
  using duration = std::chrono::duration<rep, period>;
  using time_point = std::chrono::time_point<UniversalTimeScaleClock>;
  static constexpr bool is_steady = true;
};

using Duration = UniversalTimeScaleClock::duration;
using Time = UniversalTimeScaleClock::time_point;

constexpr int64 kUtsEpochOffsetFromUnixEpochInSeconds =
    (719162ll * 24ll * 60ll * 60ll);

```

```
Duration FromSeconds(double seconds);
Duration FromMilliseconds(int64 milliseconds);

double ToSeconds(Duration duration);

Time FromUniversal(int64 ticks);
int64 ToUniversal(Time time);

std::ostream& operator<<(std::ostream& os, Time time);

```