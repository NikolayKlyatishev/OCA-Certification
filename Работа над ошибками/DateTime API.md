# DateTime API

# Основные методы

## Получение LocaDateTime

**Текущая:**

* static LocalDateTime now()

**По параметрам:**

* static LocalDateTime of(int year, Month month, int dayOfMonth, int hour, int minute)
* static LocalDateTime of(int year, Month month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond)
* static LocalDateTime of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond)
* static LocalDateTime of(LocalDate date, LocalTime time)

* static LocalDateTime ofInstant(Instant instant, ZoneId zone)

* static LocalDateTime from(TemporalAccessor temporal)

* static LocalDateTime parse(CharSequence text)
* static LocalDateTime parse(CharSequence text, DateTimeFormatter formatter)

* int getYear()
* int getMonthValue()
* Month getMonth()
* int getDayOfMonth()
* int getDayOfYear()
* DayOfWeek getDayOfWeek()
* int getHour()
* int getMinute()
* int getSecond()
* int getNano()

* LocalTime toLocalTime()

* LocalDateTime withYear(int year)
* LocalDateTime withMonth(int month)
* LocalDateTime withDayOfMonth(int dayOfMonth)
* LocalDateTime withDayOfYear(int dayOfYear)
* LocalDateTime withHour(int hour)
* LocalDateTime withMinute(int minute)
* LocalDateTime withSecond(int second)
* LocalDateTime withNano(int nanoOfSecond)

* LocalDateTime plus(TemporalAmount amountToAdd)
* LocalDateTime plus(long amountToAdd, TemporalUnit unit)
* LocalDateTime plusYears(long years)
* LocalDateTime plusMonths(long months)
* LocalDateTime plusWeeks(long weeks)
* LocalDateTime plusDays(long days)
* LocalDateTime plusHours(long hours)
* LocalDateTime plusMinutes(long minutes)
* LocalDateTime plusSeconds(long seconds)
* LocalDateTime plusNanos(long nanos)
* LocalDateTime minusYears(long years)
* LocalDateTime minusMonths(long months)
* LocalDateTime minusWeeks(long weeks)
* LocalDateTime minusDays(long days)
* LocalDateTime minusHours(long hours)
* LocalDateTime minusMinutes(long minutes)
* LocalDateTime minusSeconds(long seconds)
* LocalDateTime minusNanos(long nanos)

* String format(DateTimeFormatter formatter)

* OffsetDateTime atOffset(ZoneOffset offset)
* ZonedDateTime atZone(ZoneId zone)

* int compareTo(ChronoLocalDateTime<?> other)

* boolean isAfter(ChronoLocalDateTime<?> other)
* boolean isBefore(ChronoLocalDateTime<?> other)
* boolean isEqual(ChronoLocalDateTime<?> other)
